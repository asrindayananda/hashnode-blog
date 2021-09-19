## Import image in React JS

Below are various ways of importing an image in React JS 

- Add image to your /src directory then import image and load like below
```
import star from './star.jpg';
//In your const or function
<img src={star} alt="Girl in a jacket" width="50" height="50"/>
```

- Or you can load a url directly

```
<img src="http://clipart-library.com/images/zcXobAjqi.png" alt="Star" width="50" height="50"></img>
```

- Or you can require image after adding image to your /src directory

```
    <img src={require('./star.jpg')} alt="Star"/>
```

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

