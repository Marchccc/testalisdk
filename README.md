# testalisdk




声明：此库为个人维护的composer版本，未对官方代码做任何修改，只为方便composer安装使用。

阿里云官方sdk git库：https://github.com/aliyun/aliyun-openapi-php-sdk

阿里云官方文档：https://developer.aliyun.com/tools/sdk


一个查询直播服务录制域名配置列表的使用示例：

```
<?php
require_once "./vendor/autoload.php";

use live\Request\V20161101\DescribeLiveRecordConfigRequest;

/**
 * init aliyun core
 *
 * @author 剑心 <0x00gc@gmail.com>
 * @DateTime  2018-12-01
 * @return    object 	DefaultAcsClient
 */
function initClict()
{
	//config http proxy
	define('ENABLE_HTTP_PROXY', false);
	define('HTTP_PROXY_IP', '127.0.0.1');
	define('HTTP_PROXY_PORT', '8888');

	// read config : [$regionId, $accessKeyId, $accessSecret]
	$iClientProfile = DefaultProfile::getProfile("cn-shanghai", "******", "******************");
	return new DefaultAcsClient($iClientProfile);
}

// eg: Query live config
// doc: https://help.aliyun.com/document_detail/35420.html

$client = initClict();
$data = [];
$data['AppName'] = ****';
$data['DomainName'] = '*****.com';
try {
    $DescribeLiveRecordConfigRequest = new DescribeLiveRecordConfigRequest();
    $DescribeLiveRecordConfigRequest->setDomainName($data['DomainName']);
    $response = $client->getAcsResponse($DescribeLiveRecordConfigRequest);
} catch (\Throwable $th) {
    print_r($th);
    exit("error");
}

foreach($response->LiveAppRecordList->LiveAppRecord as $k=>$v)
{
	echo '<pre>';
    print_r($v);
	echo '</pre>';
}


/*

stdClass Object
(
    [StreamName] => *
    [CreateTime] => 2017-10-30T11:05:52Z
    [DomainName] => *****.*****.com.cn
    [RecordFormatList] => stdClass Object
        (
            [RecordFormat] => Array
                (
                    [0] => stdClass Object
                        (
                            [Format] => mp4
                            [CycleDuration] => 3300
                            [OssObjectPrefix] => record/tlive/{Date}/{StreamName}/{StartTime}_{EndTime}
                        )

                )

        )

    [OssEndpoint] => oss-cn-shanghai.aliyuncs.com
    [AppName] => tlive
    [OssBucket] => ****-****-****
    [OnDemond] => 0
)

 */
```
















