# ما هو رمز ERC-1155: مقارنة مع ERC-721

أدى وصول تطبيقات جديدة على Ethereum إلى قيام فرق التطوير بتصميم أنواع جديدة من معايير الرمز المميز. في سنواته الأولى، كان معيار الرمز المميز ERC-20، الذي يحدد كيف سيطر الرمز المميز التقليدي مثل DAI أو UNI على السوق. يتعامل هذا النهج في التشفير مع جميع الأصول على أنها قابلة للتبادل تمامًا (تُعرف باسم قابلية التبديل)، وتعمل من الناحية المفاهيمية مثل عملة مثل الدولار الأمريكي.

ومع ذلك، في الأشهر الـ 18 الماضية، استحوذت NFTs على انتباه السوق، والتي تعتمد على معيار أحدث يسمى ERC-721. يسمح هذا المعيار بإنشاء رموز مخصصة لمرة واحدة: على سبيل المثال، بطاقة تداول قابلة للتحصيل أو صورة شخصية فريدة تمامًا ولا يمكن تكرارها.

في الآونة الأخيرة، كان الاهتمام في سوق التشفير يتجه نحو معيار آخر، والذي يحتوي على مجموعة منقحة حديثًا من الخصائص - معيار الرمز المميز ERC-1155. يمكن أن يؤدي هذا الجدل حول ERC-721 مقابل ERC-1155 إلى إرباك الفرق، ومن الجدير معرفة متى يتم استخدام كل فريق. على الرغم من أن ERC-1155 هو معيار أحدث ولديه بعض الفوائد التقنية التي قد تمنحه ميزة في المستقبل، إلا أنه ليس ترقية صارمة ويختلف في بعض النواحي.

## تاريخ موجز لـ NFTs

لماذا أصبح هذا الاختيار بين المعيارين المميزين نقطة ألم؟ بعد كل شيء، تستمر العديد من مشاريع NFT اليوم في استخدام معيار ERC-721.

لم يكن النظام البيئي لإيثريوم في البداية بحاجة كبيرة لمعيار رمزي جديد. بعد كل شيء، كان معظمهم حريصين على استخدام ميزة العقد الذكي التي نالت الإشادة، والتي ميزت Ethereum في الأيام الأولى. كان إنشاء شبكة blockchain مع رمز ERC-20 المصاحب أمرًا سهلاً نسبيًا وأسفر عن ولادة العديد من المشاريع الجديدة، مثل Crypto.com و USDC من Circle.

لكن النظام البيئي Ethereum شهد تحولًا زلزاليًا عندما رأى المطورون إمكانية حالات استخدام أخرى من خلال ميزة العقد الذكي الخاصة به. على عكس الرموز القابلة للاستبدال والتي يمكن استبدالها تمامًا وتعمل بشكل مشابه لفاتورة الدولار، فإن الرموز المميزة غير القابلة للاستبدال التي حددت كل رمز مميز بشكل فريد تسمح لمجموعة من التطبيقات الجديدة. 

لكل من معايير الرمز المميز تطبيقات خاصة بهما، ومن الجدير معرفة خصائصهما الفريدة للمساعدة في تحديد أيهما سيتم تنفيذه في مشروعك.

## ما هو معيار الرمز المميز ERC-1155؟

تم تطوير معيار الرمز المميز ERC-1155 بواسطة الفريق الذي يقف وراء مشروع Enjin، والذي يركز على الحلول المستندة إلى blockchain للألعاب. قدم Enjin معيار الرمز المميز في عام 2019، وهو حل وسط بين معيار ERC-20 ومعيار ERC-721.

حدد Enjin عددًا من التحديات المرتبطة بمعيار ERC-721 المحدود نسبيًا - على وجه الخصوص، عدم القدرة على إجراء عمليات نقل الدُفعات. 

مع معيار ERC-721، إذا كان على المرء نقل عدة NFTs، فإن كل NFT يتطلب معاملة واحدة - لأن كل NFT يتم تمثيله بواسطة عقد ذكي واحد. يؤدي هذا إلى ارتفاع تكاليف المعاملات بشكل باهظ عند صك أو تداول NFTs الفردية. يسمح ERC-1155 بتحويل دفعات - أصول متعددة في عقد ذكي واحد - ينتج عنه نقل جميع الرموز المميزة في وقت واحد، مما يؤدي إلى شبكة أقل ازدحامًا وبالتالي تقليل تكاليف الغاز. على سبيل المثال، عندما يريد المستخدم بيع ألف عنصر في لعبة ما إلى مستخدم آخر، يمكنه استخدام نقل الرمز المميز الدفعي لـ ERC-1155 لإرسالها جميعًا دفعة واحدة 💸. 

ميزة رئيسية أخرى لهذا المعيار متعدد الرموز هو أنه يدعم الرموز المميزة القابلة للاستبدال وغير القابلة للاستبدال - نظرًا لقدرته على دعم حالات متعددة - على نفس العنوان والعقد. من الناحية العملية، هذا يعني أنه يمكنك إجراء مدفوعات داخل اللعبة باستخدام رمز مميز قابل للتبديل على هذا العنوان ونقل أصول NFT الفريدة في نفس الوقت أيضًا.

ميزة إضافية لـ ERC-1155 هي أنها تدعم إنشاء الرموز شبه القابلة للاستبدال. يتم تداول SFTs كرموز قابلة للاستبدال، ولكن بمجرد استردادها، يتم تحويلها إلى NFTs. على سبيل المثال، يمكن اعتبار تذكرة لحضور حفل موسيقي قبل الحدث بمثابة أصل قابل للاستبدال - ستمنحك أي تذكرة دخولًا مطابقًا لـ GA في الحفلة الموسيقية. ومع ذلك، بعد الحفلة الموسيقية، تفقد التذكرة قيمتها القابلة للتداول وتصبح عنصرًا فريدًا من التذكارات. تمكن SFTs هذا النوع من الوظائف مباشرة في رمز التذكرة نفسها. 

أخيرًا، يمكن التراجع عن عمليات نقل الرمز المميز في هذا المعيار في حالة حدوث خطأ. وفقًا لمعيار ERC-721، لا يمكنك استرداد الأصول إذا تم إرسالها إلى عنوان خاطئ. ومع ذلك، يحتوي ERC-1155 على وظيفة تعالج هذا الأمر. توجد وظيفة النقل الآمن وعدد من القواعد الأخرى لمنع الاستغلال.

## مقارنة بين ERC-721 و ERC-1155

يمكن أن يشهد معيار الرمز المميز ERC-1155 استخدامًا أكثر وضوحًا من معيار الرمز المميز ERC-721 في المستقبل القريب، وذلك بفضل ميزاته الإضافية. كلاهما يسمح لك بأن تكون قادرًا على إصدار NFTs الجديدة، ولكن هناك بعض الاختلافات الرئيسية:

- يسمح ERC-1155 بإنشاء كل من **الرموز المميزة شبه القابلة للاستبدال والرموز غير القابلة للاستبدال**، بينما يسمح ERC-721 بالأخير فقط.
- في ERC-1155، ترتبط العقود الذكية بمعرفات URI متعددة ولا **تخزن بيانات وصفية إضافية** (مثل أسماء الملفات). وبالمقارنة، فإن ERC-721 يدعم فقط البيانات الوصفية الثابتة المخزنة مباشرة على العقد الذكي لكل معرف رمز، مما يزيد من تكاليف النشر ويحد من المرونة.
- تدعم العقود الذكية الخاصة بـ ERC-1155 **عددًا لا حصر له من الرموز المميزة**، بينما يحتاج ERC-721 إلى عقد ذكي جديد لكل نوع من أنواع الرموز المميزة.
- يسمح ERC-1155 أيضًا **بالتحويلات المجمعة للرموز المميزة**، والتي يمكن أن تقلل من تكاليف المعاملات وأوقاتها. مع ERC-721، إذا كنت تريد إرسال رموز متعددة، فإنها تحدث بشكل فردي.

كما هو الحال دائمًا، إذا كانت لديك أي أسئلة أو شعرت بالتعثر أو أردت فقط أن تقول مرحبًا، فقم بالإنضمام على <a href="https://discord.gg/ykgUvqMc4Q" target="_blank">Discord</a> وسنكون أكثر من سعداء لمساعدتك!
