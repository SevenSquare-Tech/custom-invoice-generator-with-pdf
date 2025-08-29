# Laravel Invoices

This Laravel package provides an easy to use interface to generate **Invoice PDF files** with your provided data.

Invoice file can be stored, downloaded, streamed on any of the filesystems you have configured. Supports different templates and locales.

[Here's the Complete Guide to Build Custom PDF Invoice Generator in Laravel.](https://www.sevensquaretech.com/laravel-pdf-invoice-generator-guide-code-github/)

## Features

- Taxes - fixed or rate - for item or for invoice
- Discounts - fixed or by percentage - for item or for invoice
- Shipping - add shipping price to your invoices
- Automatic calculation - provide minimal set of information, or calculate yourself and provide what to print
- Due date
- Easy to customize currency format
- Serial numbers as you like it
- Templates
- Translations
- Global settings and overrides on-the-fly

## Installation

Via Composer

```bash
$ composer require laraveldaily/laravel-invoices:^4.1
```

After installing Laravel Invoices, publish its assets, views, translations and config using the `invoices:install` Artisan command:

```bash
$ php artisan invoices:install
```

### Updates

Since it is evolving fast you might want to have latest template after update using Artisan command:

```bash
$ php artisan invoices:update
```

> It will give a warning if you really want to override default resources

Or alternatively it can be done separately.

```bash
$ php artisan vendor:publish --tag=invoices.views --force
```

```bash
$ php artisan vendor:publish --tag=invoices.translations --force
```

## Available Methods

Almost every configuration value can be overrided dynamically by methods.

## Invoice

#### General

- addItem(InvoiceItem $item)
- addItems(Iterable)
- name(string)
- status(string) - invoice status [paid/due] if needed
- seller(PartyContract)
- buyer(PartyContract)
- setCustomData(mixed) - allows user to attach additional data to invoice
- getCustomData() - retrieves additional data to use in template
- template(string)
- logo(string) - path to logo
- getLogo() - returns base64 encoded image, used in template to avoid path issues
- filename(string) - overrides automatic filename
- taxRate(float)
- shipping(float) - shipping amount

#### Serial number

- series(string)
- sequence(int)
- delimiter(string)
- sequencePadding(int)
- serialNumberFormat(string)
- getSerialNumber() - returns formatted serial number

#### Date

- date(CarbonInterface)
- dateFormat(string) - Carbon format of date
- payUntilDays(int) - Days payment due since invoice issued
- getDate() - returns formatted date
- getPayUntilDate() - return formatted due date

#### Currency

- currencyCode(string) - EUR, USD etc.
- currencyFraction(string) - Cents, Centimes, Pennies etc.
- currencySymbol(string)
- currencyDecimals(int)
- currencyDecimalPoint(string)
- currencyThousandsSeparator(string)
- currencyFormat(string)
- getAmountInWords(float, ?string $locale) - Spells out float to words, second parameter is locale
- getTotalAmountInWords() - spells out total_amount
- formatCurrency(float) - returns formatted value with currency settings '$ 1,99'

#### File

- stream() - opens invoice in browser
- download() - offers to download invoice
- save($disk) - saves invoice to storage, use ->filename() for filename
- url() - return url of saved invoice
- toHtml() - render html view instead of pdf

## InvoiceItem

- make(string) - [static function] same as `(new InvoiceItem())->title(string)`
- title(string) - product or service name
- description(string) - additional information for service entry
- units(string) - measurement units of item (adds units columns if set)
- quantity(float) - amount of units of item
- pricePerUnit(float)
- discount(float) - discount in currency
- discountByPercent(float) - discount by percents discountByPercent(15) means 15%
- tax(float)
- taxByPercent(float)
- **subTotalPrice(float) - If not provided calculates itself**

## Testing

```bash
$ composer test
```

## Credit By

- [David Lun][https://github.com/mc0de]
