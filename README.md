# bubblepy
Bubble Babble Binary Data Encoding - Python library

See http://bohwaz.net/archives/web/Bubble_Babble.html for details.

Original Copyright 2011 BohwaZ - http://bohwaz.net/  
Copyleft 2015 europa - https://github.com/eur0pa
Copyright 2016 zefciu - https://github.com/zefciu

Based on :
- Bubble Babble spec: http://wiki.yak.net/589/Bubble_Babble_Encoding.txt
- Nitrxgen PHP script: http://www.nitrxgen.net/bubblebabble.php
- Bubble Babble encoder for Go: http://codereview.appspot.com/181122
- Bubble Babble class for PHP: https://github.com/bohwaz/bubblebabble

Use:

```pyshell
    >>> from bubblepy import BubbleBabble
    >>>
    >>> # Encoding simple ASCII strings
    >>> bb = BubbleBabble()
    >>> bb.encode('Pineapple')
    'xigak-nyryk-humil-bosek-sonax'
    >>> bb.decode('xigak-nyryk-humil-bosek-sonax')
    b'Pineapple'
    >>>
    >>> # To encode non-ASCI data you must encode to bytestring
    >>> bb.encode('Pchnąć w tę łódź jeża lub ośm skrzyń fig')
    Traceback (most recent call last):
        (...)
    ValueError: Non-ASCII character found. Encode your data
    >>> bb.encode('Pchnąć w tę łódź jeża lub ośm skrzyń fig'.encode('utf-8'))
    xikik-cocor-subur-fucam-dycem-lymyk-lecyn-nacen-riras-gycud-bepak-cicur-pocym-gyxex
    >>> bb.decode('xikik-cocor-subur-fucam-dycem-lymyk-lecyn-nacen-riras-gycud-bepak-cicur-pocym-gyxex').decode('utf-8')
    'Zażółć gęślą jaźń'
    >>>
    >>> # You can use Bubble Babble to encode e.g. uuids
    >>> import uuid
    >>> u1 = uuid.uuid4()
    >>> bb.encode(u1.bytes)
    'xezeg-tetor-pybyt-vuboc-gapop-boceg-todup-banyk-voxux'
    >>> u2 = uuid.UUID(bytes=bb.decode('xezeg-tetor-pybyt-vuboc-gapop-boceg-todup-banyk-voxux'))
    >>> u1 == u2
    True
    >>>
    >>> # The default alphabet can be overridden
    >>> # Consonants should be 17-letter long and vowels 6-letter long
    >>> bb2 = BubbleBabble(consonants=u'бгджзклмнпрстфхцч', vowels=u'аиоуыэ')
    >>> bb2.encode(b'0123456789')
    'читаж-гатиж-жэфиж-кыфож-мухуж-почоч'
)
```
