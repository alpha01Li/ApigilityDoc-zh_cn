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