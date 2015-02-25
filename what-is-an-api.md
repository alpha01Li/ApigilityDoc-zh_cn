ʲô��API��
==========

API��ȫ���ǡ�Application Programming Interface��Ӧ�ó����̽ӿڣ���������Ϊһ�����ָ���������ν�����

һ����˵�������ǽ����ᵽAPIʱ��ȷ�е�˵��**Web APIs**����Щͨ�����ı�����Э�鴫�����ݣ�HTTP������������ض�������£���ô��һ��APIָ��һ���û��������ʹ��һ��API�����ķ���ʲôURI����ʹ�ã�ÿ��URI����ʹ��ʲôHTTP������������ʲô��ѯ�ַ���������ʲô���ݿ��Է��͵��������壬���û����Եõ�ʲôԤ�ڵ���Ӧ��

API������
---------

Web api���Է�Ϊ������:

* **Զ�̹��̵��� (Remote Procedure Call, RPC)**
* **������״̬���� (REpresentational State Transfer, REST)**

RPC
---

RPCͨ�����ص��ǵ���URI�����ϵ����������Ա�����,ͨ��ֻͨ��`POST`������[XML-RPC](http://www.xmlrpc.com/) �� [SOAP](http://www.w3.org/TR/soap/)��ͨ������£���ᴫ��һ���ṹ�������󣬰���Ҫ���õĲ������ƺ�����Ҫ���ݸ������Ĳ�����������Ӧһ���ṹ���ĸ�ʽ��

һ�����ӣ�

    POST /xml-rpc HTTP/1.1
    Content-Type: text/xml
    <?xml version="1.0" encoding="utf-8"?>
    <methodCall>
        <methodName>status.create</methodName>
        <params>
            <param>
                <value><string>First post!</string></value>
            </param>
            <param>
                <value><string>mwop</string></value>
            </param>
            <param>
                <value><dateTime.iso8601>20140328T15:22:21</dateTime.iso8601></value>
            </param>
        </params>
    </methodCall>

����`POST`��һ����֪��URI��`/xml-rpc`�������������Ҫ���õĲ�����`status.create`���Ͳ������ݸ�������Щ�������ᰴ���������˳�򱻴��ݡ�����������£������������Ĳ�����PHP��������������

    class Status
    {
        public function create($message, $user, $timestamp)
        {
            // do something...
        }
    }


RPCͨ���Ƿǳ������Ե�;ͨ���ܺܺõ�ӳ�䵽��������Ĳ�����

����Ŀ�����Ӧ���£�

    HTTP/1.1 200 OK
    Content-Type: text/xml
    <?xml version="1.0" encoding="utf-8"?>
    <methodResponse>
        <params>
            <param><value><struct>
                <member>
                    <name>status</name>
                    <value><string>First post!</string></value>
                </member>
                <member>
                    <name>user</name>
                    <value><string>mwop</string></value>
                </member>
                <member>
                    <name>timestamp></name>
                    <value><dateTime.iso8601>20140328T15:22:21</dateTime.iso8601></value>
                </member>
            </struct></value></param>
        </params>
    </methodResponse>


���Ǵ���Ӧ�н���һ��ֵ����������������£������ڷ���ֵ���յ��ṹ�������൱��һ������������߹������顣��PHP�У���ֵ�����������ģ�

    array(
        'status' => 'First post!',
        'user' => 'mwop',
        'timestamp' => '20140328T15:22:21',
    )

��������ʱ,�����RPC��ʽ��һ�ֱ�׼�ķ�ʽ���档��XML-RPC������һ�������󡱵Ļ�Ӧ����SOAP��һ��SOAP������XML-RPC��Ϊ���ӣ��ȷ�˵������ֻ������һ����һ��ֵ���������棬��ô���ǿ��ܻ�õ�������ʾ�Ĵ�����Ӧ��

    HTTP/1.1 200 OK
    Content-Type: text/xml
    <?xml version="1.0" encoding="utf-8"?>
    <methodResponse>
        <fault><value><struct>
            <member>
                <name>faultCode</name>
                <value><int>422</int></value>
            </member>
            <member>
                <name>faultString</name>
                <value><string>
                    Too few parameters passed; must include message, user, and timestamp
                </string></value>
            </member>
            <member>
                <name>timestamp></name>
                <value><dateTime.iso8601>20140328T15:22:21</dateTime.iso8601></value>
            </member>
        </struct></value></fault>
    </methodResponse>

������һ��Ҫע����ǣ�RPCͨ��������Ӧ����������д��󱨸档HTTP״̬�벻��������ͬ������ζ������Ҫ��鷵��ֵ����ȷ���Ƿ����˴���

��󣬺ܶ�RPCʵ�ֻ�ͨ��Э�鱾���ṩ�ĵ������ǵ������û�����SOAP���ĵ���[WSDL](http://www.w3.org/TR/wsdl)����XML-RPC���ĵ���ͨ�����֡�[system.](http://tldp.org/HOWTO/XML-RPC-HOWTO/xmlrpc-howto-interfaces.html)���������������˵�����ܣ��������ǣ�������ʵ�ֺ��ṩ���������������񽻻��ı�����Ϣ��

Ҫ��סRPC��Ҫ���ǣ�

* һ������˵㣬��������
* һ������˵㣬һ��HTTP������ͨ����`POST`����
* �ṹ���ģ���Ԥ��������ʽ���ṹ���ģ���Ԥ�����Ӧ��ʽ��
* �ṹ���ģ���Ԥ��Ĳ��������ʽ��
* ���ò����Ľṹ���ĵ���

��һ��˵����RPC������һ����̫�ʺ���web APIs��
* �㲻��ȷ��ͨ��URI�ж�����Դ�ǿ��õġ�
* ȱ��HTTP���棬�޷�ʹ��ԭ��HTTP�����ڳ��õĲ�����ȱ��HTTP��Ӧ������󱨸棬��Ҫ�Խ����˼��ȷ���Ƿ����˴���
* ��һ���С��ĸ�ʽ�������ƣ��ͻ�����������л���ʽ���ܱ�ʹ�ã�����Ϣ��ʽͨ���Կ����ύ�򷵻ص���������ǿ�Ӳ���Ҫ�����ơ�

������˵�������RPC����ͨ����ʹ��web APIs��ʹ��HTTP��ַ����书�ܡ�


REST
====
��״̬���䣨Ӣ�ģ�Representational State Transfer�����REST������һ���淶������Χ��HTTP�淶��Ƶļܹ���[ά���ٿ�](http://zh.wikipedia.org/wiki/REST)�������ṩ��һ���ܺõ�REST�ĸ���ĸ������ͷḻ����Դ��

REST����HTTP�����ƣ������ڣ�
* ����ԴURI��ΪΨһ��ʶ����
* �ḻ������HTTP���ʶ���Դ�Ĳ�����
* Ϊ�ͻ���ָ����ʾ���ǿ��Գ��ֵĸ�ʽ����������Ϊ�����������Щ��������������ܽ�������
* ��Դ����ʾ��ϵ֮�����ϵ�����磬��ý�����ӡ�������HTML�ĵ�������

��̸�۹���REST��[Richardson Maturity Model](http://martinfowler.com/articles/richardsonMaturityModel.html)����������ʵ��һ��������õ�REST APIʱ��������Ҫ�Ĺ�ע��������4����Σ���0��ʼ������

* **Level 0**:
* **Level 1**:
* **Level 2**:
* **Level 3**: