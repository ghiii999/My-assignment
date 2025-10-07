sequenceDiagram
    participant العميل
    participant الخادم

    العميل->>الخادم: ClientHello (إصدار TLS، رقم عشوائي، مجموعات التشفير)
    الخادم->>العميل: ServerHello (الإصدار المختار، رقم عشوائي، مجموعة التشفير)
    الخادم->>العميل: Certificate (شهادة المفتاح العام للخادم)
    الخادم->>العميل: ServerKeyExchange (معلومات المفتاح المؤقت، موقعة)
    الخادم->>العميل: ServerHelloDone

    Note over العميل: يتحقق من شهادة الخادم
    Note over العميل: يولد المفتاح السري التمهيدي (Pre-Master Secret)

    العميل->>الخادم: ClientKeyExchange (مفتاح العميل المؤقت)
    العميل->>الخادم: ChangeCipherSpec
    العميل->>الخادم: Finished (تجزئة مشفرة للمصافحة)

    Note over الخادم: يولد المفتاح السري التمهيدي
    Note over الخادم: يفك تشفير ويتحقق من رسالة 'Finished'

    الخادم->>العميل: ChangeCipherSpec
    الخادم->>العميل: Finished (تجزئة مشفرة للمصافحة)

    Note over العميل: يفك تشفير ويتحقق من رسالة 'Finished'

    rect rgb(230, 255, 230)
        Note over العميل,الخادم: اكتملت المصافحة. يبدأ الاتصال الآمن.
        العميل<->>الخادم: بيانات تطبيق مشفرة
    end
