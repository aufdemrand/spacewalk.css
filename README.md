# spacewalk.css

A simple, modern CSS library for building web-HUDs.

## Use spacewalk.css

View the latest release at: [https://www.jsdelivr.com/package/gh/aufdemrand/spacewalk.css]

```html
<link rel='stylesheet' src='https://cdn.jsdelivr.net/gh/aufdemrand/spacewalk.css@0.8.1/spacewalk.css'>
```

## Example

```html
<html>
<head>
    <title>Guestbook</title>
    <link rel='stylesheet' src='https://cdn.jsdelivr.net/gh/aufdemrand/spacewalk.css@0.8.1/spacewalk.css'>
</head>
<body>

  <header>
    <a href='/'>
      <img src='assets/logo.svg' style='width: 10em;'>
    </a>
  </header>

  <main>

    <details open class='bordered padded-more white centered narrow-width'>
        <summary class="pointer"><strong>Make a new Guestbook</strong></summary>
        <p class='more-block-margin text-spaced'>
            Enter the details of your event to provide a guestbook to your visitors.
        </p>
        <panel>
            <form action='index.html' method='POST'>
                <input name='name' required
                       type='text'
                       autocomplete='off'
                       placeholder='Enter the name of your event'>
                <label for='email'>Your email:</label>
                <input name='email'
                       id='email'
                       type='email'
                       placeholder='Optional'>
                <flex class='spread'><span></span><button type='submit'>Done</button></flex>
            </form>
        </panel>
    </details>
    
    <panel class='narrow-width centered way-more-bottom-margin padded'>

        <h6 class='way-more-top-margin'>Your guestbooks:</h6>

        <div class='way-less-block-margin'>
            <a href='/guestbooks/graduation-party'>
                <strong>Julia's Graduation Party</strong>
            </a>
        </div>
        <div class='way-less-block-margin'>
            <a href='/guestbooks/tech-meetup'>
                <strong>July Tech Meet-up</strong>
            </a>
        </div>
    </panel>

  </main>

  <footer>
      <span>Made with spacewalk.css</span>
  </footer>

</body>
</html>


