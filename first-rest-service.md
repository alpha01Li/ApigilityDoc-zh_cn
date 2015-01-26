REST����̳�
===========

����һ��REST����
����һ���У����ǽ�����һ���򵥵�REST����

����
----
���¼ٶ����Ѿ��Ķ�����ѭ[��װָ��](http://vergil.cn/archives/3/)��[����ƪ](http://vergil.cn/archives/13/)������㻹û�У������֮ǰ���ġ�

����Ҫ��װ������`zfcampus/statuslib-example`ģ������ɱ��̡̳���ѭ��Щ���裺

����1
-----

�����Ӧ�ó���ĸ�Ŀ¼��ִ�����£�

	$ php composer.phar require "zfcampus/statuslib-example:~1.0-dev"

����2
-----

�༭�ļ�`config/application.config.php`�������`StatusLib`ģ�飺

	array(
		'modules' => array(
		/* ... */
		��StatusLib',
		),
		/* ... */
	)

����3
-----

����һ��php�ļ�`data/statuslib.php`������һ�����飺

	<?php
	return array();
ȷ�����ļ���web server�û���д��

����4
-----

�༭�ļ�`config/autoload/local.php`������������ã�

	return array(
		/* ... */
		'statuslib' => array(
		'array_mapper_path' => 'data/statuslib.php',
		),
	);

����5
-----

����㽫��Ҫһ����Ч��HTTP������֤�ļ���ͨ��Ϊ`htpasswd`�����������һ��ʹ��[Apache�ṩ�ı�׼htpasswd����](http://httpd.apache.org/docs/2.2/programs/htpasswd.html)������ʹ��һ��[����htpasswd������](http://www.htaccesstools.com/htpasswd-generator/)���洢`htpasswd`�ļ�������Ӧ�ó���`data/htpasswd`����ע����ʹ�õ�ƾ���Ա��Ժ����ʹ�����ǡ�

һ����Щ������ɣ������̡̳�

����
----

��Apigility���ĵ��У��ر�������һ���У�ʹ���������

* ʵ�壨Entity����
����һ����Ѱַ�ʵ����һ��URI��Ψһ��ʶ����

* ���ϣ�Collection����
һ���Ѱַ��ʵ�塣ͨ������£������а���������ʵ�嶼����ͬ���͵ģ����ҹ�����ͬ�Ļ���URI��Ϊ���ϡ�

* ��Դ��Resource����
���մ�����������ݣ�һ������ȷ��һ�����ϻ�ʵ���Ƿ���URI��ȷ��������ȷ����ʲô������ִ�С�

* ������ӣ�Relational Links����
һ��URI�������������Ĺ�ϵ��Դ��ص����ӡ���������������ͬ��ʵ��ͼ���֮��Ĺ�ϵ���Լ�ֱ�����ӵ����ǣ�ʹweb�ͻ��˿��Զ���Щ��ϵ���в�������Щ��ʱҲ��ý������ӡ�

REST���񷵻�ʵ��ͼ��ϣ����ṩ��ص�ʵ��ͼ���֮��ĳ�ý�����ӡ���Դ�����Э���ж���������ʵ��ͼ��ϡ�

����һ��REST����
---------------

�ڱ����У����ǽ�����һ��REST����ʾ����

��������APIs��ҳ�棬Ȼ��������ǰ����½��д����ġ�Status��API����һ����ѡ��REST Services���˵��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-rest-services.png)

�����Create New REST Service����ť
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-new-rest-service.png)

����Ի���������ѡ���һ���Ǵ�����Code-Connected���������ӣ���������һ���Ǵ�����DB-Connected�����ݿ����ӣ�������

> ### Code-Connected vs DB-Connected services
> ���㴴��һ���������ӷ���Apigility����������REST��������п��õĸ��ֲ��������ԭ�ģ�stub "Resource" class������Դ���ࡣ��Щ�������ء�405 Method Not Allowed������Ӧ��ֱ������д���Լ��Ĵ��롣���������ӡ�������ζ���㽫�ṩִ�����API��ʵ�ʹ����еĴ���; Apigility�ṩ���ڱ�¶�ô�����Ϊһ��API���ߡ�
>
���ݿ����ӷ���������ָ��һ�����ݿ���������һ�����ݱ�Ȼ��Apigility����һ�������⡱��Դ��������ί�в������ײ��`Zend\Db\TableGateway\TableGateway`ʵ�������仰˵����������Ӧ�ó��򿪷���rapid application development��RAD����ԭ�͹��ߡ�

�������ϰ�����ǽ������������ӡ��ڡ�REST Service Name�����롰Status����Ȼ�󰴡�Create Code-Connected REST Service����һ������ɹ������󣬵������д�š�Status������ɫ������չ�������Բ鿴����
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-status-settings.png)

Apigility�ṩ���������Ĭ��ֵ��

* ����ֻ����`GET`����ȡ�б���`POST`��������ʵ�壩������
* ʵ������`GET`����ȡʵ�壩��`PUT`���滻ʵ�壩��`PATCH`��ִ�в��ָ��£���`DELETE`��ɾ��ʵ�壩������
* �����ļ���֧�ַ�ҳ������Apigility������Ϊÿҳ25����Դ��
* Apigility����һ�����ڷ������Ƶ�·��URI�����磬`/status[/:status_id]`��

> ### URI·��
> Apigility������Zend Framework 2 MVC�ܹ�֮�ϣ��������ʹ����[·������](http://framework.zend.com/manual/2.3/en/modules/zend.mvc.routing.html)��
>
> ͨ��Apigility���ɵ�·�ɶ�����ν�ġ�Segment��·�ɡ��������㣺
>
> * ָ��URI�Ŀ�ѡ���֣�ʹ��`[]`�﷨��
> * ָ����������ʹ��`:varName`��`:var_name`ƥ�䡣
> * ָ��������ƥ��;û��һ�����������������ţ�`{}`���ڱ���Ϊ�����֡�
>
> ����REST���񣬸�URI���ɶ�ǿ����ƥ���䱾������档���ɵ���ָ��������Ϊһ�����ϡ�������������У���·����`/Status`��Ҳ��һ�����������Ŀ�ѡ���֣���Ϊ��ʵ���ʶ������[/:status_id]���⽫��ƥ����`/status/foo`, `/status/2`, `/status/96fa5ac9-3ae2-45b2-84d5-c346936be292`������URI��
>
> ע�⣺����URI��ָ����ʵ��URIʱ�����ƶ�ʵ��֮���/���㲻����б�ߣ�/�����󼯺ϡ�
> Ϊʲô����ΪREST����ּ��һ��URI����һ����Դ�������������һ��б�ߣ�/�������ǻᱻ������URI����������ͬ����Դ��


չ����REST Parameters�����֣���ῴ����Ϊ��Hydrator Service Name�����ֶκ�`Zend\Stdlib\Hydrator\ArraySerializable`��ֵ������Ҫ�ı���������`StatusLib`ʾ���⹤����

����������ڸ÷���ı������ϳ�����ɫ�ġ�edit����ť�������Ȼ��չ����REST Parameters�����֡��ڡ�Hydrator Service Name��ѡ�ѡ��Zend\Stdlib\Hydrator\ObjectProperty��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-settings-edit.png)

> ### Hydrators
> Hydrators�Ƕ���������һ���������鵽һ���ض��Ķ������ͣ���֮��Ȼ��ÿ��hydratorʹ���˲�ͬ�Ĳ��ԣ����������һ�㡣Apigilityʹ��Ĭ�ϵ�hydrator������
`ArraySerializable`������Ŀ��ʵ������������
> 
> * `getArrayCopy()` ���ڻ�ȡһ������ĸ���
> * `exchangeArray($array)` ���ڹ���һ���������
>
> ����Щ������ʹ�ú�PHP��`ArrayObject`һ������
>
> `ObjectProperty` hydrator����һ������ĸ���ʱ����ȡ��������й������ԣ��͹������ʱ������������Ĺ������ԡ�

�����ǵ�ʾ���У�`StatusLib`���ṩ�Լ���ʵ���ͼ����ࡣͨ�����������չ����Service Class Names����壬���ұ༭��Entity Class���ֶζ�ȡ`StatusLib\Entity`�͡�Collection Class���ֶζ�ȡ`StatusLib\Collection`��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-settings-classes.png)

> ### Service Classes
> ���㴴��һ���������ӵķ���ApigilityΪ��������4��PHP���ļ���
>
> * һ��ʵ���ࡣ
> * һ��������̳���Zend\Paginator\Paginator���⽫���������ṩ��ҳ�������
> * һ����Դ������ִ�в�����
> * һ�����������ڴ�����Դ��
>
> ��Ĵ�������Ѿ�ȷ����ʵ����ͼ����࣬������������ɵغ���Apigility�����Ĵ����stub���ָࣨ����Apigility���ɵ��ࣩ������ע�⣺��������հ汾��API������ܻᷢ�����ض��汾��ʵ��ͼ�������������õġ���Ϊ���ǿ��������ģ����ÿ���ض��İ汾��¶��ֻ�����뱩¶�����ԡ�

���ڣ�ѡ����Ļ�ײ�����ɫ��Save����ť��
��һ�������Ƕ���һЩ�ֶκ����ǵ�API�ĵ���

�������ǵķ�����ֶ�
------------------

���ǽ������ֶΣ�

* `message` - ״̬��Ϣ���������Ƿǿյģ����Ҳ�����140���ַ���
* `user` - �û��ṩ��״̬��Ϣ���������Ƿǿյģ���������һ��������ʽ��
* `timestamp` - ���͵�ʱ����������Ǳ����ύ�ģ�������ύ��ֻ�������֡�����������Ӧ�з��ء�

����Ҳ����һ��`id`���ֶΣ�����ֻ��Ϊ��չʾ��

��������Fields��ѡ���Ȼ��༭������ɫ�ġ�Edit����ť������ͨ�������ͣ�ڷ���ı������ҵ���
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-fields-edit.png)

����Ϊ��Field name�����ı���������롰message����Ȼ��`�س�`�������µ��ֶΡ�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-field.png)

���ڣ���ͬ���ķ���������user���͡�timestamp���ֶ�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-all-fields.png)

������С�message������ɫ��������λ����չ������
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-edit.png)

�ڡ�Description���������������롰A status message of no more than 140 characters.��״̬��Ϣ���ܳ���140���ַ��������ڡ�ValidationValidate Failure Message����֤ʧ����Ϣ���������롰A status message must contain between 1 and 140 characters.��״̬��Ϣ�������1��140���ַ�������

�������ͣ�ڡ�Filters�����������������Ұ���Add Filter����ťչʾ��Add Filter��������ѡ���ѡ��`Zend\Filter\StringTrim`����ʾ�����롰trim������Сѡ��Χ���󰴡�Add Filter����ť������Cancel����ťɾ�������Աߵġ�Add Filter����ť��ɡ�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-filter-trim.png)

���ڣ��������ͣ�ڡ�Validators����֤��������������Ȼ�󰴡�Add Validator����ť��չʾ��Add Validator��������ѡ���ѡ��`Zend\Validator\StringLength`����ʾ�����롰string������Сѡ��Χ���󰴡�Add Validator����ť������Cancel����ťɾ�������Աߵġ�Add Validator����ť��ɡ�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-validator-length.png)

�������ͣ��`Zend\Validator\StringLength`������չʾ��Add Option����ť����������ڳ��ֵ�ѡ�����ѡ��`max`�����ֵ����ѡ�к�ͻ�����µı�������ֵ��140����Ȼ������Add Option����ť������Cancel����ťɾ�������Աߵġ�Add Option����ť��ɡ�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-validator-max.png)

���ʱ����Ӧ���������Ļ�Ͽ������£�
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-message-complete.png)

�����message���ֶα��������۵�����

�����ʱ������һ����ϰ��

* ���¡�user���ֶΣ�
	* �����������The user submitting the status message.��
	* �����֤ʧ����Ϣ����"You must provide a valid user.��
	* ���`Zend\Filter\StringTrim`������
	* ���`Zend\Validator\Regex`��֤��������һ��`pattern`ѡ���ֵ`/^(mwop|andi|zeev)$/`�������Ҫ���������滻������������ֻ��ǳƣ�
* ���¡�timestamp���ֶΣ�
	* �����������he timestamp when the status message was last modified.��
	* �����֤ʧ����Ϣ����You must provide a timestamp.��
	* �л���Required�����Ϊ��No��
	* ���`Zend\Validator\Digits`��֤��

��ɺ�����Ļ�����½ǰ���ɫ�ġ�Save Changes����ť����ɺ�ġ�user���͡�timestamp���ֶο������������½�ͼ��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-user-complete.png)
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-timestamp-complete.png)

������ת�Ƶ��ĵ���

�ĵ�
----

REST����������ĵ���������ͨ��HTTP����������ͨ��HTTP����Ϊÿ�����Ϻ�ʵ�塣

���ڼ�¼һ��REST����Ĺ��̾�����������[����ָ��](http://vergil.cn/archives/13/)ѧ��ģ�����������֮ͬ����

* �㽫��ҪΪ**ÿ��**���Ϻ�ʵ���HTTP���������ĵ���
* ��Щ������Ԥ�ڻ��������ݣ���������ҪΪ�������ݴ����ĵ���

�������Ѿ���¼������ֶΡ���generate from configuration���������ã�����ť�����ɵ�ǰ�������Ӧ�������ļ�����ᷢ�֣���Ӧ�ĸ��ذ���`_links`��`_embedded`��Ա��������Ϊ��Apigility REST����Ĭ��ʹ��[��ý��Ӧ������](http://stateless.co/hal_specification.html)��Hypermedia Application Language�� HAL����ʽ�����ṩ��һ��Ϊ�����ӵ�������¶���ķ����Լ�������Ƕ�����Դ�����й�HAL�ĸ�����Ϣ�����Ķ����ǵ�[HAL����](https://apigility.org/documentation/api-primer/halprimer)��

����������ϰ��¼���Ϻ�ʵ��Ĳ�����

* �ṩ���������������ͻ�ȡ״̬��Ϣ��������ĵ�
* �ṩ"״̬��Ϣ�Ĳ����б�"�ļ����ĵ�
	* ����`GET`��������������Ϊ����ȡ״̬��Ϣ�ķ�ҳ�б�
	* ����`POST`��������������Ϊ������һ���µ�״̬��Ϣ��
* �ṩ�������ͻ�ȡ������Ϣ����ʵ���ĵ�
	* ����`GET`��������������Ϊ����ȡ״̬��Ϣ��
	* ����`POST`��������������Ϊ������״̬��Ϣ��
	* ����`PUT`��������������Ϊ���滻״̬��Ϣ��
	* ����`DELETE`��������������Ϊ��ɾ��״̬��Ϣ��

����`DELETE`������ÿ��������ʹ�á�generate from configuration���������ã�����ť�������������Ӧ���á������Ը�⣬����Ա༭���ǣ����������Ļ�����̳̾�û�б�Ҫ�ˡ�

�Ժ����ǽ�����ĵ������ڣ������Ǽ�������֤����Ȩ��

��֤����Ȩ
---------

�����Authorization���˵��������Ȩҳ�档��ῴ��һ�������HTTP�ı���Լ�һ�����棬��ʾ���ǻ�û���趨��֤��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-authorization.png)

���������Ⱥ�����Щ���档���ı������`POST`��`PATCH`��`PUT`��`DELETE`,��ʾ���з���¶������Щ��������Ҫ��Ȩ��Ȼ������ɫ�ġ�Save����ť��
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-authorization-complete.png)

ѡ�еķ����ͷ�����Ҫ��Ȩ������ζ�������޷����ʣ������û����ṩ��Ч��ƾ�ݡ�����㳢��ִ��������ʱ��ǵĲ�������ᷢ���㲻��ִ�У����õ�һ��`403 Forbidden`����Ӧ��

���ԣ��������Ǽ��������֤���þ�����ṩһ�����ӵ���authentication screen���������
![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-authentication.png)

����������У����ǽ�ʹ��HTTP������HTTP Basic�������֤����ˣ������HTTP Basic����ť��

����ʹ����ͬ��ֵ��Ϊռλ������д��Authentication Realm����ֵΪ`api`����Location of htpasswd file����ֵΪ`data/htpasswd`����ɺ󣬵����ɫ�ġ�Save����ť��

�����Ѿ�����������ǵ�API...�������ǻ�û�к����ǵĴ�����ϵ��һ���أ���ʱ������Щ�ˡ�


������Դ
--------

����Ի���һ�£�֮ǰApigilityΪ���Ǵ�����4���࣬�ֱ���ʵ�壨entity�������ϣ�collection������Դ��resource����������factory������һ��������ʼ����Դ����ʱ���һЩ���������ǵ���Դ���ˡ�

Apigility�ṩ�汾���ơ�����������ռ�Ҳ�ǰ汾���ġ�������������㲢�����ж���汾��API��

��`module/Status/src/Status/V1/Rest/Status/StatusResource.php`�ҵ����ǵ���Դ���ļ����ڱ༭��������

���������ĵ�һ���ı��ǵ���`StatusLib\MapperInterface`�ࡣ�������`use`�����һ��`use StatusLib\MapperInterface;`��

	use StatusLib\MapperInterface;
	use ZF\ApiProblem\ApiProblem;
	use ZF\Rest\AbstractResourceListener.php;

��һ�������Ǹ��ඨ��һ��`protected`����`$mapper`��

	class StatusResource extends AbstractResourceListener
	{
    	protected $mapper;

����һ�����캯��������һ��`MapperInterface`����������������`$mapper`���ԡ�

	protected $mapper;
    public function __construct(MapperInterface $mapper)
    {
        $this->mapper = $mapper;
    }

���ڣ���������ӳ������ɣ���������дһЩ������

* �滻`create()`�����ķ�����Ϊ`return $this->mapper->create($data);`��
* �滻`delete()`�����ķ�����Ϊ`return $this->mapper->delete($id);`��
* �滻`fetch()`�����ķ�����Ϊ`return $this->mapper->fetch($id);`��
* �滻`fetchAll()`�����ķ�����Ϊ`return $this->mapper->fetchAll();`��
* �滻`patch()`�����ķ�����Ϊ`return $this->mapper->update($id, $data);`��
* �滻`update()`�����ķ�����Ϊ`return $this->mapper->update($id, $data);`��

���ע�⵽���ǲ�û�и������е����з������м��ַ��������ڶ��б�Ĳ��������ǲ���ȷ����Щ������

������λ�ȡ`$mapper`����Դ��Ϊ�ˣ����ǽ��޸����ǵĹ������ڱ༭�����ļ�`module/Status/src/Status/V1/Rest/Status/StatusResourceFactory.php`���޸��������������������£���Ӧ��ֻ��`__invoke()`���������޸�`return`����

	<?php
	namespace Status\V1\Rest\Status;
	class StatusResourceFactory
	{
    	public function __invoke($services)
    	{
        	return new StatusResource($services->get('StatusLib\Mapper'));
    	}
	}

������һ��������ʹ����[Zend Framework 2 Service Manager]��http://framework.zend.com/manual/2.3/en/modules/zend.service-manager.intro.html��������ķ�������ѡ�����������������һ�����е�`StatusResource`ʵ�����ڸ÷����У����ǰ�`Statuslib`ģ�����Ѿ�����ĵ���һ��������ע�뵽���ǵ�`StatusResource`��

������ϣ�����������һ���ɹ�����REST����

������ִ��һЩ����������������ι����ġ�


����
----

��һ���������ǽ�`GET`���󵽼���

	GET /status HTTP/1.1
	Accept: application/json

���ǻ�û������κ�״̬��Ϣ���������ǵõ���һ���ռ��ϵ���Ӧ��

	HTTP/1.1 200 OK
	Content-Type: application/hal+json
	{
    	"_embedded": {
        	"status": []
    	},
    	"_links": {
        	"self": {
            	"href": "http://localhost:8888/status"
        	}
    	},
    	"page_count": 0,
    	"page_size": 25,
    	"total_items": 0
	}

�����ǳ������һЩ�

	POST /status HTTP/1.1
	Accept: application/json
	Content-Type: application/json
	{
    	"message": "First post!",
    	"user": "mwop"
	}

���ǵ����������������֤����Ȩ�𣿺��ˣ����ڿ��Կ������Ĺ�����

	HTTP/1.1 403 Forbidden
	Content-Type: application/problem+json
	{
    	"detail": "Forbidden",
    	"status": 403,
    	"title": "Forbidden",
    	"type": "http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html"
	}

�������ṩƾ֤�������ʹ�õ�HTTP�ͻ��ˣ���cURL��HTTPie����REST�ͻ��˻�Postman����һ���������ִ�����ƾ�ݣ�Ȼ������Ǳ��һ��`Authorization`ͷ����ῴ��������һ���������`Basic` token��

    POST /status HTTP/1.1
    Accept: application/json
    Authorization: Basic bXdvcDptd29w
    Content-Type: application/json
    {
        "message": "First post!",
        "user": "mwop"
    }

���ڳɹ��ˣ�

    HTTP/1.1 201 Created
    Content-Type: application/hal+json
    {
        "_links": {
            "self": {
                "href": "http://localhost:8888/status/3c10c391-f56c-4d04-a889-bd1bd8f746f0"
            }
        },
        "id": "3c10c391-f56c-4d04-a889-bd1bd8f746f0",
        "message": "First post!",
        "timestamp": 1396709084,
        "user": "mwop"
    }

> ע�⣺ÿ��ʵ��ı�ʶ����Ψһ�ģ����㴴��һ�����µ�״̬��Ϣ�����в�ͬ�ı�ʶ����

�������һ�status��Ϣ�����ǿ���ʹ��URI��`self`��ϵ�������ҵ�����

	GET /status/3c10c391-f56c-4d04-a889-bd1bd8f746f0 HTTP/1.1
	Accept: application/json

    HTTP/1.1 200 OK
    Content-Type: application/hal+json
    {
        "_links": {
            "self": {
                "href": "http://localhost:8888/status/3c10c391-f56c-4d04-a889-bd1bd8f746f0"
            }
        },
        "id": "3c10c391-f56c-4d04-a889-bd1bd8f746f0",
        "message": "First post!",
        "timestamp": 1396709084,
        "user": "mwop"
    }

����ص����ǵļ���URL������ʲô��

	GET /status HTTP/1.1
	Accept: application/json

    HTTP/1.1 200 OK
    Content-Type: application/hal+json
    {
        "_embedded": {
            "status": [
                {
                    "_links": {
                        "self": {
                            "href": "http://localhost:8888/status/3c10c391-f56c-4d04-a889-bd1bd8f746f0"
                        }
                    },
                    "id": "3c10c391-f56c-4d04-a889-bd1bd8f746f0",
                    "message": "First post!",
                    "timestamp": 1396709084,
                    "user": "mwop"
                }
            ]
        },
        "_links": {
            "first": {
                "href": "http://localhost:8888/status"
            },
            "last": {
                "href": "http://localhost:8888/status?page=1"
            },
            "self": {
                "href": "http://localhost:8888/status?page=1"
            }
        },
        "page_count": 1,
        "page_size": 25,
        "total_items": 1
    }

������������status;����PATCH���������Ϣ��

	PATCH /status/3c10c391-f56c-4d04-a889-bd1bd8f746f0 HTTP/1.1
	Accept: application/json
	Content-Type: application/json
	{"message": "[Updated] First Post!"}

��ѽ!���ַ�����Ҫ��֤!

    HTTP/1.1 403 Forbidden
    Content-Type: application/problem+json
    {
        "detail": "Forbidden",
        "status": 403,
        "title": "Forbidden",
        "type": "http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html"
    }

�������ƾ�ݣ�

    PATCH /status/3c10c391-f56c-4d04-a889-bd1bd8f746f0 HTTP/1.1
    Accept: application/json
    Authorization: Basic bXdvcDptd29w
    Content-Type: application/json
    {"message": "[Updated] First Post!"}

�ɹ���


    HTTP/1.1 200 OK
    Content-Type: application/hal+json
    {
        "_links": {
            "self": {
                "href": "http://localhost:8888/status/3c10c391-f56c-4d04-a889-bd1bd8f746f0"
            }
        },
        "id": "3c10c391-f56c-4d04-a889-bd1bd8f746f0",
        "message": "[Updated] First post!",
        "timestamp": 1396709724,
        "user": "mwop"
    }

`PUT`����������`PATCH`��ͨ�����������ṩһ��������`�滻`��ʵ�塣�������ǲ���չʾ����

�����ǳ���һ��`DELETE`���󡣻���һ�£�������Ҫ��Ȩ�ġ��������ǵ�һʱ���ṩƾ�ݡ�

    DELETE /status/3c10c391-f56c-4d04-a889-bd1bd8f746f0 HTTP/1.1
    Accept: application/json
    Authorization: Basic bXdvcDptd29w

�⽫���£�

	HTTP/1.1 204 No Content

�����ǿ�һ���ĵ���


�ĵ�
----

��ǰһ�º�������Ǵ������ĵ����������Admin UI�￴��������ܻῴ��Ƕ����ÿ��������ĵ���Ȼ�����㻹���Կ��ĵ�����

�ڶ���������һ����Ϊ��API Docs���������

![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-api-docs.png)

����API���ĵ��汾�����ҿ���Ϊÿ���汾�ֱ�鿴�ĵ��������v1�����ӡ�

![](https://apigility.org/apigility-documentation/img/intro-first-rest-service-api-docs-api.png)

�����չ��ÿ�����������չ��һ��������ʾ�����������Ӧ��ϸ�ڲ�������������`Accept`��`Content-Type`����ͷ��Ԥ��`Content-Type`��Ӧ��Ԥ����Ӧ״̬�룬�ȵȡ�


��Ҫ
----

����һ��,����������:

* ����һ��REST����
* �������ֶδ�������������֤��,���а���Ϊ�����ṩ���á�
* ����ķ���д�ĵ�
* Ϊ��ķ����ṩ�����֤����Ȩ��

Apigility��һ��ǿ������Ĺ��ߣ�Ϊ�㶨��API���Լ���¶���ǣ����ṩһ���������Ӵ������ṩ�ĵ������Ѿ��Ӵ������棬������ʱ��ȥ̽��������Ϊ����ô������