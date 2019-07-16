
# curl

```php
# 访问链接
function curl_file_get_contents($durl, $data = null, $tout = 30, $c_out = 10, $is_detail = false)
{
    if (empty($durl)) {
        return false;
    }
    $ch = curl_init();
    curl_setopt($ch, CURLOPT_URL, $durl);
    curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, $c_out);
    curl_setopt($ch, CURLOPT_TIMEOUT, $tout);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt($ch, CURLOPT_HEADER, false);
    if ($data) {
        curl_setopt($ch, CURLOPT_POST, 1);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
    }
    $r = curl_exec($ch);
    $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
    $errno = curl_errno($ch);
    curl_close($ch);

    if ($is_detail) {
        return array(
            'code' => $httpCode,
            'content' => $r,
            'error' => $errno,
        );
    }

    if ($httpCode != 200) {
        return false;
    }
    return $r;
}
```
