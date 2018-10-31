---

## jQuery

It's 2018. Go away.

Note:

- Modern browsers have everything built in to replace jQuery features
- jQuery might have a more succinct syntax, but browsers are faster.
- IE11 still may need some polyfills (e.g. for Fetch)

+++

### DOM Selection

```javascript
$('#app');
document.getElementById('app');

$('.my #awesome selector');
document.querySelectorAll('.my #awesome selector');

$(el).find(selector);
el.querySelectorAll(selector);
```

+++

### DOM Manipulation

```javascript
$(el).addClass('is-visible');
el.classList.add('is-visible');

$(parent).append(el);
parent.appendChild(el);

$(el).attr('tabindex', 3);
el.setAttribute('tabindex', 3);

$(el).html('foo bar');
el.innerHTML = 'foo bar';

$(el).css('border-width', '20px');
el.style.borderWidth = '20px';
```

+++

### AJAX

```javascript
fetch('http://example.com/movies.json')
    .then((res) => res.json())
    .then(function (json) {
        console.log(JSON.stringify(json));
    });
    .catch(function (error) {
        console.error('Error:', error);
    });
```

@[2](Promise after success, will convert response to a JSON object)
@[3-5](Promise after the previous promise, reads the JSON object)
@[6-8](Catches any errors thrown, e.g. 404/500 errors or a throw by a previous `then` clause)

Replaces `$.ajax`, `$.get`, `$.post`. MDN provides polyfill for IE11.

+++

### Events

```javascript
$(el).on('click', onClickHandler);
el.addEventListener('click', onClickHandler);

$(el).off('click', onClickHandler);
el.removeEventListener('click', onClickHandler);
```

+++

### No Longer Needed! Unless ...

You are using a third party jQuery component.

@fa[frown-o]

Note:
- Later we'll see how to integrate a jQuery component such as the Lookup or bootstrap-datepicker into a React component

+++

### More Examples

* http://youmightnotneedjquery.com/
* https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
