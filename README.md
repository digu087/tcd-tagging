Laravel Taggable Trait
============

[![Latest Stable Version](https://poser.pugx.org/digu087/tcd-tagging/v/stable.svg)](https://packagist.org/packages/rtconner/laravel-tagging)
[![Total Downloads](https://poser.pugx.org/digu087/tcd-tagging/downloads.svg)](https://packagist.org/packages/rtconner/laravel-tagging)
[![License](https://poser.pugx.org/digu087/tcd-tagging/license.svg)](https://packagist.org/packages/rtconner/laravel-tagging)




This package is a fork of rtconner/laravel-tagging . This is a custom version of the original package. It adds ability for tags to be associated with multiple groups

#### Composer Install (for Laravel 5/6/7 and Lumen 5/6/7)

```shell
composer require digu087/tcd-tagging "~4.0"
```

#### Install and then Run the migrations

The package should auto-discover when you composer update. Then publish the tagging.php and run the database migrations with these commands.

```bash
php artisan vendor:publish --provider="Conner\Tagging\Providers\TaggingServiceProvider"
php artisan migrate
```

#### Setup your models
```php
class Article extends \Illuminate\Database\Eloquent\Model
{
	use \Conner\Tagging\Taggable;
}
```

#### Quick Sample Usage

```php
$article = Article::with('tagged')->first(); // eager load

foreach($article->tags as $tag) {
	echo $tag->name . ' with url slug of ' . $tag->slug;
}

$article->tag('Gardening'); // attach the tag

$article->untag('Cooking'); // remove Cooking tag
$article->untag(); // remove all tags

$article->retag(array('Fruit', 'Fish')); // delete current tags and save new tags

$article->tagNames(); // get array of related tag names

Article::withAnyTag(['Gardening','Cooking'])->get(); // fetch articles with any tag listed

Article::withAllTags(['Gardening', 'Cooking'])->get(); // only fetch articles with all the tags

Article::withoutTags(['Gardening', 'Cooking'])->get(); // only fetch articles without all tags listed

Conner\Tagging\Model\Tag::where('count', '>', 2)->get(); // return all tags used more than twice

Article::existingTags(); // return collection of all existing tags on any articles
```

[Documentation: More Usage Examples](docs/usage-examples.md)

[Documentation: Tag Groups](docs/tag-groups.md)

[Documentation: Tagging Events](docs/events.md)

[Documentation: Tag Suggesting](docs/suggesting.md)

### Configure

[See config/tagging.php](config/tagging.php) for configuration options.

###### Lumen Installation

[Documentation: Lumen](docs/lumen.md)

#### Upgrading Laravel 4 to 5

This library stores full model class names into the database. When you upgrade laravel and you add namespaces to your models, you will need to update the records stored in the database.
Alternatively you can override Model::$morphClass on your model class to match the string stored in the database.

#### Credits

 - Robert Conner - http://smartersoftware.net

#### Further Reading
 - [Laravel News article on tagging with this library](https://laravel-news.com/how-to-add-tagging-to-your-laravel-app)
 - [3rd Party Posting on installation with Twitter Bootstrap 2.3](http://blog.stickyrice.net/archives/2015/laravel-tagging-bootstrap-tags-input-rtconner)
