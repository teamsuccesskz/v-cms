# V-CMS

A modular **Content Management System** built on **Laravel** using the [`nwidart/laravel-modules`](https://github.com/nWidart/laravel-modules) package.  
The system is designed to be extendable, maintainable, and developer-friendly, allowing you to build custom modules quickly.

---

## ✨ Features

- 📦 **Modular architecture** powered by `nwidart/laravel-modules`
- ⚡ **Laravel 9+ / PHP 8.0+** support
- 🎨 **Vue 3 frontend integration**
- 🗄 **PostgreSQL 15+ / MySQL 8+** support
- 🔑 **Role & permission management**
- 📝 **Built-in admin panel** for content and user management
- 📚 **Auto-generated API documentation** via [Scribe](https://scribe.knuckles.wtf/laravel/)

## ✨ How to install locally

1. Install and run `composer` via Docker: 
   ```bash 
    docker run --rm -u "$(id -u):$(id -g)" -v "$(pwd):/var/www/html" -v ~/.ssh:/home/index/.ssh -w /var/www/html $(docker build --no-cache --build-arg uid=$(id -u) --build-arg gid=$(id -g) -q .) /usr/bin/composer install --ignore-platform-reqs
   ```
2. Setup alias for `Laravel Sail`:
   ```bash 
    alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
   ```
3. Up containers:
   ```bash
    ./vendor/bin/sail up -d
   ```
4. Install frontend dependencies:
   ```bash
    sail npm i
   ```
5. Run dev server for `hot-reload`:
   ```bash 
    sail npm run dev
   ```

## ✨ Example

````php
public static function defineStructure(): ModelStructure
{
  return ModelStructure::create()
      ->addField(
          StringField::create()
              ->setName('title')
              ->setTitle('Title')
              ->identify()
              ->required()
              ->showInFilter()
              ->showInSearch()
              ->setGroup('main_info')
      )
      ->addField(
          BoolField::create()
              ->setName('show')
              ->setTitle('Active')
              ->setTooltip('Show on the website')
              ->showInFilter()
              ->hideFromEditor()
      )
      ->addField(
          DateField::create()
              ->setName('date')
              ->setTitle('Date')
              ->setDefaultValue(date('Y-m-d'))
              ->showInFilter()
      )
      ->addField(
          SelectField::create()
              ->setName('type')
              ->setTitle('Type')
              ->setOptions([
                  'type1' => 'Type 1',
                  'type2' => 'Type 2',
                  'type3' => 'Type 3'
              ])
              ->showInFilter()
              ->setGroup('additional_info')
      )
      ->addField(
          PointerField::create()
              ->setName('author')
              ->setTitle('Author')
              ->required()
              ->setModel(Author::class)
              ->filterCondition("name like '%*title*%'")
              ->modal()
              ->showInFilter()
              ->showInSearch()
              ->setGroup('additional_info')
      )
      ->addField(
          FileField::create()
              ->setName('file')
              ->setTitle('File')
              ->hideFromEditor()
      )
      ->addField(
          ImageField::create()
              ->setName('image')
              ->setTitle('Image')
      )
      ->addField(
          TextField::create()
              ->setName('short_description')
              ->setTitle('Short description')
      )
      ->addField(
          HtmlField::create()
              ->setName('full_description')
              ->setTitle('Full description')
              ->hideFromEditor()
      )
      ->addField(
          PointerField::create()
              ->setName('parent')
              ->setTitle('Parent post')
              ->setModel(\Modules\Blog\Entities\News::class)
              ->hideFromEditor()
              ->parent()
      )
      ->setSortable()
      ->setRecursive()
      ->setModelTitle('News')
      ->setRecordTitle('post')
      ->setAccusativeRecordTitle('post');
}
````
