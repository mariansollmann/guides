# Style

## Formatting
* Every file should end with a EOL
* EOL is \n
* Use two spaces for indentation (look around you, some projects use tabs).
* Use the IntelliJ IDEA codestyle templates!

## Naming
* Do not use **abbreviations** (for exceptions: capitalize them like normal words. E.g. `Css`)
* If the individual item as well as a **collection of items** is used, suffix the collection with "List". E.g. `eggList`.
* Chose **systematic names** reading from *general* to *specific* from left to right, rather than grammatically correct names. E.g. `streamChannelMessageType` or `ratingAverage`).
* **Methods** usually begin with a verb. E.g. `getSomething`, `setSomething`, `deleteSomethingElse`

## PHP
### Template: Cache
```php
$cacheKey = CM_CacheConst::Some_Constant . '_foo:' . $foo . '_bar:' . $bar;
if (false === ($result = CM_Cache::get($cacheKey))) {
	// Assign $result somehow

	CM_Cache::set($cacheKey, $result);
}
```

### Template: Random md5 string
32 characters hexadecimal
```php
md5(rand() . uniqid());
```

### Template: Exception
```php
throw new CM_Exception_NotAllowed('Parameter `' . $param . '` is not allowed.');
```

### Coding standards
* Internal types: Use type-safe comparison, cast/check early.
* Use type hinting whenever possible. Prefer objects to internal types as arguments.
* Usage of "ternary operator" is discouraged, but allowed in simple non-nested variable assignments, like:
```php
$state = isset($requestBody['state']) ? (string) $requestBody['state'] : null;
```
* Within classes, we define first the class constants, then the non-static class properties, the static class properties, the constructor, the abstract methods, the non-static methods and finally the static methods. Within each category, items are ordered by their visibility (starting with the highest one) and finally sorted alphabetically. The only exception to the alphabetical sorting are setters, which should be defined right after their respective getter.

Some/Example.php
```php
<?php

abstract class Some_Example {

	const FOO = 1;

	/** @var int */
	private $_fooBar;

	/** @var bool */
	public static $enabled;

	/**
	 * @param int $fooBar
	 */
	public function __construct($fooBar) {
		$this->_fooBar = (int) $fooBar;
	}

	/**
	 * @return float|null
	 */
	abstract public function getSome();

	/**
	 * @return bool
	 */
	public function getPublic() {
	}

	/**
	 * @param bool $state
	 * @param bool|null $foo
	 * @param string[]|null $bar
	 */
	public function setPublic($state, $foo = null, array $bar = null) {
		if (null === $foo) {
			$foo = false;
		}
		if (null === $bar) {
			$bar = array();
		}
	}

	/**
	 * @return bool|int|float|string|array|Object|Object[]
	 */
	private function _getPrivate() {
		if (true) {
			return true;
		} else {
			return 'hallo' . PHP_EOL;
		}
		return false;
	}

	/**
	 * @return Some_Example
	 */
	public static function getElse() {
		return new static(12);
	}
}
```
## HTML / CSS / JS
### Coding Standards
* HTML/CSS: <a href="http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml">Use Google Code Style Guide</a>
* Use CamelCase
* Use "-" for related child selectors (e.g. "clipSlide" & "clipSlide-handle")
* Use exclusive CSS class for JS bindings

### Example (toggleNext jQuery Plugin)
#### HTML
```html
<div class="toggleNext">Some Link</div>
<div class="toggleNext-content">
	Some Content
</div>
```
#### CSS
```css
.toggleNext {
	cursor: pointer;
}

.toggleNext-content {
	display: none;
}
```
#### JS
```js
(function($) {
	$.fn.toggleNext = function() {
		return this.each(function() {
			var $toggler = $(this);
			var content = $toggler.next('.toggleNext-content');

			if (!content.length || $toggler.data('toggleNext')) {
				return;
			}

			var icon = $('<span />').addClass('icon toggle');
			$toggler.prepend(icon);

			if ($toggler.hasClass('active')) {
				icon.addClass('active');
				content.show();
			}

			$toggler.on('click.toggleNext', function() {
				$toggler.toggleClass('active');
				icon.toggleClass('active');
				content.slideToggle(100);
			});
			$toggler.data('toggleNext', true);
		});

	};
})(jQuery);
```

## Translations
### Heading Letter Case (for Headings, Menus, Tooltips, Buttons,...)
First and last word, as well as all open class words capitalized:
* Nouns
* Main verbs (not auxiliary verbs: be (am, are, is, was, were, being), can, could, do (did, does, doing), have (had, has, having), may, might, must, shall, should, will, would)
* Adjectives
* Adverbs
* Interjections

#### Examples
* The Vitamins are in my Fresh California Raisins.
* Terms of Use

### Add Translation
Use this translation method for words, short reusable sentences.
```smarty
{translate 'Some cool phrase'}
```
```smarty
{translate 'Some cool phrase with {$variable}' variable=$variable}
```
### Add Key Translation
Use this translation method for internal generated words, long texts, unique sentences.
```smarty
{translate '.language.key'}
```
```php
<?php
$langauge = CM_Model_Language::findByAbbreviation('en');
$language->setTranslation('.language.key', 'Translation without variables');
```

### Add Translation with Variables
```smarty
{translate '.language.key' variable=$variable}
```
```php
<?php
$language = CM_Model_Language::findByAbbreviation('en');
$language->setTranslation('.language.key', 'Transalation with {$variable}');
```

### Delete Translation
```php
<?php
CM_Model_Language::deleteKey('Some cool phrase');
CM_Model_Language::deleteKey('Some cool phrase with {$variable}');
CM_Model_Language::deleteKey('.language.key');
```
