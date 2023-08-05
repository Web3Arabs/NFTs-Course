# إنشاء مشروع NFT بإستخدام IPFS

سيقوم هذا المشروع بتوفير NFTs للمستخدمين بحيث يتمكن كل شخص من سك NFT

## المتطلبات الاساسية للبدء في هذا الدرس:

1. يمكنك التعامل مع لغة البرمجة JavaScript.
2. انتهيت من قرأة درس <a href="/courses/d64bee08-2e38-4ad5-958e-5ab6c42ebb41/lessons/9ac6f6b5-8ed0-462d-b0c5-374f1e1d0db3" target="_blank">اساسيات لغة Solidity</a>.
3. انتهيت من قرأة درس <a href="/courses/253cff7d-f8ee-4a42-8e2f-d865d2589393/lessons/a334390a-c893-4720-9fa2-f9d828f14947" target="_blank">ما هو بروتوكل IPFS؟</a>

## العقد الذكي

سنقوم بإستخدام عقود OpenZeppelin وهي عبارة عن مكتبة لتطوير العقود الذكية الآمنة. يتضمن أكثر عمليات التنفيذ أمانًا واختبارًا للمعايير المشتركة مثل الرموز المميزة ERC20 و ERC721. كما أنه يوفر أنماطًا آمنة للترقية، مما يسمح لك بنشر العقود الذكية وتحديثها بشكل آمن. بالإضافة إلى ذلك، يتميز بواجهة برمجة تطبيقات مستقرة، مما يعني أن عقودك لن تنكسر بشكل غير متوقع عند الترقية إلى إصدار ثانوي أحدث.

يُستخدم العقد Ownable.sol لتنفيذ الملكية في عقودك. ويوفر آليات أساسية للتحكم في الوصول، مما يسمح لك بتقييد وظائف معينة لمالك العقد فقط. كما يوفر أيضًا مفتاح إيقاف تشغيل اختياريًا قابلًا للتعيين من قبل المالك، مما يسمح للمالك بإيقاف العقد من قبول أي معاملات أخرى، والسماح للمالك باستعادة أي أموال متبقية.

العقد ERC721Enumerable.sol هو عقد يضيف طرق تمديد يمكن عدها إلى معيار ERC721. يتيح ذلك سهولة الوصول إلى بيانات الرمز المميز، مثل عدد الرموز المميزة التي يمتلكها عنوان، وبيانات تعريف رمزية محددة، والمزيد... بالإضافة إلى ذلك، يضيف العقد أيضًا طريقة لنقل العديد من الرموز المميزة في وقت واحد.

العقد Strings.sol يوفر العديد من وظائف معالجة السلاسل. يتضمن وظائف لمقارنة السلاسل، والتحقق مما إذا كانت السلسلة فارغة، والحصول على طول السلسلة

### بناء العقد

> قبل كل شيء يفضل ان تقوم بأخذ نظرة كاملة على <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol" target="_blank">عقد ERC721 لكي يكون لديك معرفة جيدة في التعامل معه</a>

سنستخدم احد الادوات التي ستساعدنا في التعامل مع العقود الذكية وهي Hardhat. يعتبر Hardhat هي بيئة وإطار تطوير شبكة Ethereum مصمم للتعامل بشكل كامل مع لغة Solidity.

سنقوم بإنشاء مشروع بإسم W3ArabsProject والذي سيحتوي على تطبيق Hardhat وعقدنا الذكي.

```bash
mkdir W3ArabsProject
cd W3ArabsProject/
```

سنقوم بإعداد npm في التطبيق وتثبيت Hardhat

```bash
npm init --yes
npm install --save-dev hardhat
npm install --save-dev @nomicfoundation/hardhat-toolbox@2
npm install @openzeppelin/contracts
```

سنقوم الان بتشغيل تطبيق Hardhat

```bash
npx hardhat
```

#### سنلاحظ ان التطبيق يحتوي على 3 مجلدات رئيسية وهي:

1. contracts: الذي سنقوم من خلاله بكتابة العقود الذكية.
2. scripts: والذي سنقوم من خلاله بالتعامل مع العقود الذكية او رفعها على الشبكات.
3. test: والذي سنقوم من خلاله بإجراء اختبارات لعقدنا الذكي.

يمكنك الان البدء في إنشاء عقدك الذكي. قم بإنشاء ملف في مجلد contracts بإسم W3ArabsProject.sol

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Enumerable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Strings.sol";

contract W3ArabsProject is ERC721Enumerable, Ownable {
    // parameters إلى سلاسل عند تمريرها كمعلمات uint256 يشير إلى أنه سيتم تحويل قيم
    using Strings for uint256;

    // لكل رمز مميز URI يتم استخدام هذا المتغير لتخزين
    string _tokenURI;

    // 0.01 يقوم بتخصيص قيمة للرمز المميز وهي
    uint256 public _price = 0.01 ether;

    // إجمالي عدد الرموز المميزة التي تم قبضها
    uint256 public tokenIds;

    /**
    * لتحديد اسم ورمز لمشروعنا ERC721 يُستخدم
    * _tokenURI الخاص بمشروعنا في المتغير baseURI يتم تمرير
    */
    constructor (string memory baseURI) ERC721("W3ArabsProject", "W3AP") {
        _tokenURI = baseURI;
    }

    // NFT تسمح هذه الدالة للمستخدم بقبض 1
    function mint() public payable {
        // يجب ان يمتلك المستخدم ايثير بقيمة اكثر من او يساوي 0.01
        require(msg.value >= _price, "You have not a ether");
        // NFT في كل مرة يقوم المستخدم بسك tokenIds يقوم بزيادة
        tokenIds += 1;
        _safeMint(msg.sender, tokenIds);
    }

    function _baseURI() internal view virtual override returns (string memory) {
        return _tokenURI;
    }

    function tokenURI(uint256 tokenId) public view virtual override returns (string memory) {
        _requireMinted(tokenId);

        string memory baseURI = _baseURI();
        return bytes(baseURI).length > 0 ? string(abi.encodePacked(baseURI)) : "";
    }

    function withdraw() public onlyOwner {
        address _owner = owner();
        uint256 amount = address(this).balance;
        (bool sent, ) =  _owner.call{value: amount}("");
        require(sent, "Error to send Ether");
    }

    receive() external payable {}

    fallback() external payable {}
}
```

> كل ما تحتاجه الان لاكمال عقدك الذكي هو كتابة الوظائف التي تريد تشغليها في داخل العقد الذكي كما تريد ان يعمل العقد الذكي الخاص بك

دعنا نقوم بتوضيح بعض function التي استخدمت في العقد الذكي

```solidity
function _baseURI() internal view virtual override returns (string memory) {
    return _tokenURI;
}
```

تقوم الدالة ()baseURI_ بتجاوز الدالة ()baseURI_ التي توفرها Openzeppelin، والتي تُرجع افتراضيًا سلسلة فارغة. تُرجع الدالة الجديدة ()baseURI_ قيمة tokenURI__ وهي متغير مخزن في العقد ويمكن للمالك تعيينه. يسمح هذا للمالك بتعيين URI أساسي لاستخدامه كقاعدة لجميع URIs المميزة.

```solidity
function tokenURI(uint256 tokenId) public view virtual override returns (string memory) {
    _requireMinted(tokenId);

    string memory baseURI = _baseURI();
    return bytes(baseURI).length > 0 ? string(abi.encodePacked(baseURI)) : "";
}
```

تقوم الدالة ()tokenURI بتجاوز الدالة ()tokenURI التي توفرها Openzeppelin، والتي تأخذ uint256 tokenId كوسيطة وتعيد سلسلة تحتوي على رمز URI. تتطلب وظيفة tokenURI أن يكون tokenId قد تم سكه مسبقًا وستعيد baseURI المتسلسل مع tokenId إذا لم يكن baseURI فارغًا.

```solidity
function withdraw() public onlyOwner {
    address _owner = owner();
    uint256 amount = address(this).balance;
    (bool sent, ) =  _owner.call{value: amount}("");
    require(sent, "Error to send Ether");
}
```

يستخدم لسحب الأموال من عقد ذكي. يحصل أولاً على عنوان مالك العقد باستخدام وظيفة المالك (). ثم يحصل على مقدار إيثر الذي يحتفظ به العقد حاليًا باستخدام العنوان (هذا). تعبير التوازن. ثم يستدعي الرمز وظيفة call () على عنوان المالك، ويمرر مقدار Ether كمعامل قيمة. أخيرًا، يتحقق للتأكد من إرسال إيثر بنجاح، ويعطي خطأ إذا لم يكن كذلك.

```solidity
receive() external payable {}

fallback() external payable {}
```

تُستخدم دالة ()receive لتلقي إيثر من مصادر خارجية ، مثل من المستخدمين الذين يرسلون المعاملات إلى العقد.

تُستخدم دالة ()fallback للتعامل مع أي معاملات أخرى تدخل في العقد ، مثل استدعاءات الوظائف غير الموجودة.

> يتم تمييز كلتا الوظيفتين على أنهما قابلان للدفع، مما يعني أنهما يمكنهما قبول الأثير كجزء من مدخلاتهما

### رفع NFT والبيانات الوصفية على IPFS

سنقوم بإستخدام منصة <a href="https://filebase.com" target="_blank">Filebase</a> من اجل ان نقوم برفع الملفات على IPFS ونتحكم بها بكل سهولة.

قم بإنشاء حساب على <a href="https://console.filebase.com/signup" target="_blank">Filebase</a> ومن ثم قم بفتح *Buckets*

<img src="https://www.web3arabs.com/courses/create-buckets-filebase.png" alt="Filebase Buckets"/>

قم بإنشاء Buckets وتسميته. يمكنك رفع صورة NFT التي تود استخدامها في الرمز المميز.

بعد ان قمت برفع صورة NFT ستحتاج الى إضافة البيانات البيانات الوصفية. قم بإنشاء ملف في جهازك بإسم metadata.json وقم بإضافة هذا

```json
{
    "description": "This NFT I've deployed an ERC721 Smart Contract on Rinkeby",
    "external_url": "https://alchemy.com",
    "image": "https://ipfs.filebase.io/ipfs/add_your_ipfs_cid",
    "name": "ERC721 PUG",
    "attributes": [
        {
            "trait_type": "Coolness",
            "value": "A lot"
        },
        {
            "trait_type": "W3A",
            "value": "web3arabs.com"
        },
        {
            "trait_type": "Token",
            "value": "ERC721"
        }
    ]
}
```

يمكنك الحصول على IPFS CID من هنا

<img src="https://www.web3arabs.com/courses/ipfs-cid-filebase.png" alt="Filebase IPFS CID"/>

يمكنك التعديل على البيانات الوصفية كما تريد ومن ثم قم برفعها على نفس Buckets الذي قمت بإنشائه سابقاً.

يمكنك الان رفع عقدك الذكي بكل سهولة. سنقوم باستخدام شبكة الاختبارات وهي sepolia. اذهب الى المجلد scripts وقم بإنشاء ملف بإسم deploy.js

```js
const hre = require("hardhat");

async function main() {
  /**
    لنشر عقود ذكية جديدة getContractFactory يستخدم
  */
  const w3arabsContract = await hre.ethers.getContractFactory("W3ArabsProject");

  // Filebase البيانات الوصفية التي قمنا برفعها على URI هنا نقوم برفع العقد وندخل
  const w3arabs = await w3arabsContract.deploy("https://ipfs.filebase.io/ipfs/add_your_ipfs_cid");

  // انتظر حتى تنتهي عملية الرفع
  await w3arabs.deployed();

  // طباعة عنوان العقد المنشور
  console.log("W3ArabsProject deployed to:", w3arabs.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

الان ستحتاج الى مزود عقدة يتيح لك الاتصال بالعديد من سلاسل الكتل المختلفة. يمكنك استخدام <a href="https://alchemy.com/" target="_blank">Alchemy</a> كمزود للعقد الخاصة بك بكل سهولة.

قم بإنشاء حساب في منصة <a href="https://alchemy.com/" target="_blank">Alchemy</a> وإذا كان لديك حساب بالفعل قم بتسجيل الدخول وقم بإنشاء تطبيق (CREATE APP) وقم بكتابة اسم لتطبيقك وتحديد شبكة (Sepolia) وقم بالنقر على (CREATE APP) ومن ثم قم بنسخ رابط المفتاح (HTTPS).

**ملاحظة**: يمكن الحصول على بعض العملات التي تساعدك في اختبار ونشر تطبيقاتك على شبكة **Sepolia** من <a href="https://sepoliafaucet.com/" target="_blank">**Alchemy Faucet**</a>

<img src="https://www.web3arabs.com/courses/alchemy-build.png" alt="Alchemy build"/>

يمكنك الحصول على (Private Key) انقر فوق النقاط الثلاث ، وانقر فوق (Account Details) ثم (Export Private Key).

<img src="https://www.web3arabs.com/courses/alchemy-keys.png" alt="Alchemy keys"/>

قم بإضافة كل ما قمت بنسخه في ملف (.env)

```bash
ALCHEMY_HTTPS_URL="add-alchemy-http-url-here"

PRIVATE_KEY="add-private-key-here"
```

قم بتثبيت حزمة dotenv حتى تتمكن من إستيراد ملف .env

```bash
npm install dotenv
```

قم بفتح ملف hardhat.config.js وقم باستيراد المفاتيح المتواجدة في ملف .env وقم بإختيار الشبكة التي تريد استخدامها لرفع العقد الذكي الخاص بك ولكننا هنا سنستخدم شبكة sepolia فلذلك سنقوم بتحديدها

```js
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config({ path: ".env" });

const ALCHEMY_HTTPS_URL = process.env.ALCHEMY_HTTPS_URL;
const PRIVATE_KEY = process.env.PRIVATE_KEY;

module.exports = {
  solidity: "0.8.9",
  networks: {
    sepolia: {
      url: ALCHEMY_HTTPS_URL,
      accounts: [PRIVATE_KEY],
    },
  },
}
```

قم بتجميع العقد الذكي الخاص بك الان. تأكد من انك في مسار تطبيقك (W3ArabsProject) وقم بتشغيل هذا الامر

```bash
npx hardhat compile
```

```bash
npx hardhat run scripts/deploy.js --network sepolia
```

<br/>

> قم بحفظ عنوان عقدك الذكي حتى نتمكن من استخدامه اثناء جعله يعمل في الواجهة الامامية.

يمكنك الان الانتقال الى الدرس التالي وربط عقدك الذكي بالواجهة الامامية 🚀
