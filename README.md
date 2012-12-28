# market.js

  Market is a text-to-HTML conversion language based upon markdown, and IRC.

  It is plain text formatting, with a strict set of rules so that basic expressions or lexers can be made without worry of creating overtly complex logic rules.

## Philosophy

  1. Market should be readable.
  2. Each feature should have no ties to other features unless they are directly related such as links.
  3. No optional flexibility, each feature must have a reason to exist and optional existance complicates that.
  4. Each feature should be able to be turned on or off.

## Plugins

  Market should be a core with the possibility of add-ons, as such there are add, remove functions to allow others to modify and change the language as they see fit and contribute back if wanted or you can make it your own if wished.

## The Core Language

  Market once again to iterate quickly, is refined, simple, and very strict to it's core.

## Newlines

  Double space will cause the section or content to be wrapped in paragraph tags `<p>` and `</p>`.

#### Rules

  1. Excess whitespace must be stripped.
  2. Excess newlines must be stripped before appending the ending tag.

### Emphasis

  Market treats emphasis differently than markdown, there are to seperate ways to emphasis and this is bold and italics, as such they have different connentations in the human langauge and should be treated as such through text for readability and for a direct and clear understanding without need for a second look.

#### Rules

  1. Must be surrounded by either a space, single character, or word to be converted.
  2. Should not intefere with links, or code, thus those should be converted and stored first, then replaced later.

#### Bold

  Text wrapped with asterisks (*) is implied as important and will be wrapped with an HTML `<strong>` tag:

  ```market
  This *is* readable.
  ```

  would produce:

  ```html
  This <strong>is</strong> readable.
  ```

#### Italics

  Text wrapped with the forward slash (/) character will be replaced with an HTML `<em>` tag:

  ```market
  Hello /World/!
  ```

  would produce:

  ```html
  Hello <em>World</em>!
  ```

### Underlined

  Text wrapped with the low-dash (_) will be raplaced with an HTML `<u>` tag:

  ```market
  I think you _should_ be able to understand what I am trying to convey.
  ```

  would produce:

  ```html
  I think you <u>should</u> be able to understand what I am trying to convey.
  ```

## Code

  Market only supports inline-code in it's core specification.

  Text wrapped with back-ticks (`) will be converted, stored, and replaced later as inline code:

  ```market
  Hello to use market at its base: `market(source, options)`
  ```

  will produce:

  ```html
  Hello to use market at it's base: <code>market(source, options)</code>
  ```

## The Plugin Language

  Market seperates it's core from it's more verbose features such as lists, links, and so forth.

### Lists

  Unlike markdown which allows for a variety of flexibility market is more refined and only allows two types of lists and markup for them to keep consistency.

  These are all future functionality, and prone to change as they have not yet been written.

#### Un-ordered

  Text with leading dashes (-) are considered un-ordered lists, the reason we don't use asterisks and I would love to include that functionality is because it would go against the core philosophies of market as they are already used for more meaningful elements.

  ```market
  Grocery List:

  - Dairy
  -- Milk
  -- Butter
  -- Eggs
  - Veggies
  -- Broccoli
  -- Carrots
  -- Lettuce
  ```

  would produce:

  ```html
  Grocery List:
  <ul>
    <li>Dairy
      <ul>
        <li>Milk</li>
        <li>Butter</li>
        <li>Eggs</li>
      </ul>
    </li>
    <li>Veggies
      <ul>
        <li>Broccoli</li>
        <li>Carrots</li>
        <li>Lettuce</li>
      </ul>
    </li>
  </ul>
  ```

#### Ordered

  Market utilizes the same paradigm as markdown for ordered lists ([A-Z0-9].)

  ```market
  Things to do:

  1. Make market specification
  2. Write out lexer
  3. Release
  ```

  would produce:

  ```html
  Things to do:
  <ol>
    <li>Make market specification</li>
    <li>Write out lexer</li>
    <li>Release</li>
  </ol>
  ```

## Github Features

  Market in it's core used to support github issues, commits, gist referencing, and more.

  Now they've been put into the plugins section.

### Issue Referencing

  Referencing github issues is a very basic syntax of `ghi:[Github Name]/[Github Repository]:[Issue Number]`

  ```market
  Hello on ghi:Nijikokun/market:83, I see you closed and commited, why?
  ```

  would produce:

  ```html
  Hello on issue <a href="http://github.com/Nijikokun/market/issues/83">#83</a>, I see you closed and commited, why?
  ```

#### Multiple Issue References

  ```market
  ghi:[Github Name]/[Github Repository]:[Number],[Number]...
  ```

  would produce:

  ```html
  issues <a href="#">#n</a>, <a href="#">#n</a>...
  ```