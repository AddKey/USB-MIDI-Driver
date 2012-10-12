Android USB MIDI �h���C�o
====

Android USB�z�X�gAPI���g�����AUSB MIDI�̃h���C�o�ł��B

- root�s�v
- �W���I��USB MIDI�f�o�C�X(�V�[�P���T��y��Ȃ�)���T�|�[�g
- �v���g�R����USB MIDI�ȁA��W����USB MIDI�@����T�|�[�g
 - YAMAHA, Roland, MOTU�̃f�o�C�X���ڑ��ł��܂�(���A�[���Ƀe�X�g����Ă��܂���)

����
----
- ��x��1�̃f�o�C�X�����ڑ��ł��܂���B

�K�v�Ȃ���
----
- Android : OS�o�[�W����3.1�ȍ~(API Level 11)�ŁAUSB�z�X�g�̃|�[�g�����邱�ƁB
- USB MIDI(�݊���)�f�o�C�X

�f�o�C�X�̐ڑ�
----
```
Android [USB A�|�[�g]------[USB B�|�[�g] USB MIDI �f�o�C�X
```

�v���W�F�N�g
----
- ���C�u����  
 - MIDIDriver : �{���C�u�����B

- �T���v��
 - MIDIDriverSample : ���C�u�������g���Ď��������A�V���Z�T�C�U�EMIDI�C�x���g���K�[�̗�

���C�u�����v���W�F�N�g�̎g����
----
�v���W�F�N�g�̐ݒ�

- ���C�u�����v���W�F�N�g��clone���܂��B
- Eclipse�̃��[�N�X�y�[�X�Ƀ��C�u�����v���W�F�N�g���C���|�[�g���A�r���h���܂��B
- �V����Android Project���쐬���A�v���W�F�N�g�̃��C�u�����Ƀ��C�u�����v���W�F�N�g�� �ǉ����܂��B
- `jp.kshoji.driver.midi.activity.AbstractMidiActivity` ���I�[�o�[���C�h����Activity�����܂��B
- AndroidManifest.xml �t�@�C���� activity �^�O��ύX���܂��B
 - **intent-filter** android.hardware.usb.action.USB_DEVICE_ATTACHED �� **meta-data** �� �I�[�o�[���C�h���� Activity �ɑ΂��Ēǉ����܂��B
 - Activity�� **launchMode** �� "singleTask" �ɂ��܂��B

```xml
        <activity
            android:name=".MyMidiMainActivity"
            android:label="@string/app_name"
            android:launchMode="singleTask" >
            <intent-filter>
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" />
            </intent-filter>
    
            <meta-data
                android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED"
                android:resource="@xml/device_filter" />
        </activity>
```

MIDI �C�x���g�̎�M

- MIDI�C�x���g���������郁�\�b�h (`"onMidi..."` �Ƃ������O)���������܂��B

MIDI �C�x���g�̑��M

- `MIDIOutputDevice`�̃C���X�^���X���擾���邽�߂ɁAAbstractMidiActivity ��`getMidiOutputDevice()`���\�b�h���Ăт܂��B
 - ���̃C���X�^���X��`"onMidi..."` �Ƃ������O�̃��\�b�h���ĂԂ�MIDI�C�x���g�����M�ł��܂��B

Maven�Ŏg��
----
maven-android-plugin���g���ɂ́AMaven 3.0.4�ȍ~���K�v�ł��B
Android�A�v����Maven���g���ăr���h������@�ɂ��āA�ڂ����́umaven-android-plugin�v�v���W�F�N�g��wiki���Q�Ƃ��Ă��������B http://code.google.com/p/maven-android-plugin/wiki/GettingStarted

- Eclipse����V�KMaven�v���W�F�N�g���쐬���܂��B
- �uAndroid 3.1�v�̈ˑ�����maven����C���X�g�[�����܂��B������̃c�[�����g���Ă��������B https://github.com/mosabua/maven-android-sdk-deployer
- �쐬�����v���W�F�N�g�� `pom.xml` �t�@�C�����ȉ��̂悤�ɕҏW���܂��B(�T���v���v���W�F�N�g�� `pom.xml` ���Q�l�ɂ��Ă݂Ă�������)�B

```xml
    <repositories>
        <repository>
            <id>midi-driver-snapshots</id>
            <url>http://github.com/kshoji/USB-MIDI-Driver/raw/master/snapshots</url>
        </repository>
    </repositories>
    
    <dependencies>
        <dependency>
            <groupId>jp.kshoji</groupId>
            <artifactId>midi-driver</artifactId>
            <version>${project.version}</version>
            <type>apklib</type>
        </dependency>
        
        <dependency>
            <groupId>android</groupId>
            <artifactId>android</artifactId>
            <version>3.1_r3</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
```

���C�Z���X
----
[Apache License, Version 2.0][Apache]
[Apache]: http://www.apache.org/licenses/LICENSE-2.0
