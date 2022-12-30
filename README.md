# AsyncAwaitPHP
```
// pertama install GuzzleHttp menggunakan composer
composer require guzzlehttp/guzzle
```
```
 "Async/Await merupakan sebuah fitur yang digunakan untuk menangani Promise supaya request data terpenuhi"
 note: // $urlenp => url endpoint (ex: http://localhost/api/enp)
```
## Codeigniter 3
```php
<?php
defined('BASEPATH') or exit('No direct script access allowed');

class AsyncModel extends CI_Model
{
    public function __construct()
    {
        parent::__construct();

        // method baru
        $this->req = new \GuzzleHttp\Client();
    }
    public function get($urlenp)
    {
        // get data api dengan async await
        $dataReq = $this->req->getAsync($urlenp)->then(function ($data) {
            return $data;
        });
        $iniResp = $dataReq->wait();
        $data = array(
            "status" => $iniResp->getStatusCode(),
            "res" => \json_decode($iniResp->getBody()),
        );
        return $data;
    }
    public function post($urlenp, $data)
    {
        // post data api dengan async await
        $dataReq = $this->req->postAsync($urlenp, [
            'headers' => [
                'Content-Type: application/json',
            ],
            'json' => $data,
        ]);
        $iniResp = $dataReq->wait();
        $res = array(
            "status" => $iniResp->getStatusCode(),
            "res" => \json_decode($iniResp->getBody()),
        );
        return $res;
    }
}
```
### Codeigniter 4
```php
<?php
namespace App\Models;
use CodeIgniter\Model;
class AsyncModel extends Model{
	..// sesudah $protected blok
  public function __construct(){
		$this->req = new \GuzzleHttp\Client();
	}
	public function get($urlenp)
    	{
		// get data api dengan async await
		$dataReq = $this->req->getAsync($urlenp)->then(function ($data) {
		    return $data;
		});
		$iniResp = $dataReq->wait();
		$data = array(
		    "status" => $iniResp->getStatusCode(),
		    "res" => \json_decode($iniResp->getBody()),
		);
		return $data;
    	}
    	public function post($urlenp, $data)
    	{
		// post data api dengan async await
		$dataReq = $this->req->postAsync($urlenp, [
		    'headers' => [
			'Content-Type: application/json',
		    ],
		    'json' => $data,
		]);
		$iniResp = $dataReq->wait();
		$res = array(
		    "status" => $iniResp->getStatusCode(),
		    "res" => \json_decode($iniResp->getBody()),
		);
		return $res;
    	}
}
```
