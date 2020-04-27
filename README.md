# phpQuery-single
phpQuery onefile composer.Continuous maintenance,Welcome PR.

`QueryList` base on phpQuery: https://github.com/jae-jae/QueryList

phpQuery单文件版本,持续维护，欢迎PR.
> phpQuery项目主页:http://code.google.com/p/phpquery/

`QueryList`是基于phpQuery的采集工具: https://github.com/jae-jae/QueryList

## Composer Installation
Packagist: https://packagist.org/packages/jaeger/phpquery-single
```
composer require jaeger/phpquery-single
```

## Usage
```php
$html = <<<STR
<div id="one">
    <div class="two">
        <a href="http://querylist.cc">QueryList官网</a>
        <img src="http://querylist.cc/1.jpg" alt="这是图片">
        <img src="http://querylist.cc/2.jpg" alt="这是图片2">
    </div>
    <span>其它的<b>一些</b>文本</span>
</div>        
STR;

$doc = phpQuery::newDocumentHTML($html);

$src = $doc->find('.two img:eq(0)')->attr('src');

echo $src;
// http://querylist.cc/1.jpg
```

## Notes Copyed From https://code.google.com/archive/p/phpquery/ and only simple formated

### INITIALIZE IT
```php
$doc = phpQuery::newDocumentHTML($markup); //OR...
$doc = phpQuery::newDocumentXML();  //OR...
$doc = phpQuery::newDocumentFileXHTML('test.html');  //OR...
$doc = phpQuery::newDocumentFilePHP('test.php');  //OR...
$doc = phpQuery::newDocument('test.xml', 'application/rss+xml'); // this one defaults to text/html in utf8  //OR... 
$doc = phpQuery::newDocument('<div/>'); //Choose anyway to Initialize!
```

### FILL IT
```php
// array syntax works like ->find() here 
$doc['div']->append('<ul></ul>'); // array set changes inner html 
$doc['div ul'] = '<li>1</li><li>2</li><li>3</li>';
```

### MANIPULATE IT
```php
// almost everything can be a chain 
$li = null; 
$doc['ul > li']
    ->addClass('my-new-class')
    ->filter(':last')
    ->addClass('last-li') // save it anywhere in the chain 
    ->toReference($li);
```

### SELECT DOCUMENT
```php
pq(); // is using selected document as default ...OR 
phpQuery::selectDocument($doc); 
// documents are selected when created or by above method 
// query all unordered lists in last selected document 
pq('ul')->insertAfter('div');
```
### ITERATE IT
```php
// all LIs from last selected DOM 
foreach(pq('li') as $li) { // iteration returns PLAIN dom nodes, NOT phpQuery objects 
    $tagName = $li->tagName; 
    $childNodes = $li->childNodes; // so you NEED to wrap it within phpQuery, using pq(); pq($li)->addClass('my-second-new-class'); 
}
```
### PRINT OUTPUT
```php
// 1st way print 
phpQuery::getDocument($doc->getDocumentID()); 

// 2nd way print 
phpQuery::getDocument(pq('div')->getDocumentID()); 

// 3rd way print 
pq('div')->getDocument(); 

// 4th way print 
$doc->htmlOuter(); 

// 5th way print 
$doc; 

// another... 
print $doc['ul']; 
```
