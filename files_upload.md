# Files Upload 

## Packages

1. multer - a multipart/form-data bodies parser

2. uuid - for random-generated ID 

## Usage 

### Backend 

1. Configure Storage

Specify where to save the data and how files name should be saved.

```js
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    /*
      Files will be saved in the 'uploads' directory. Make
      sure this directory already exists!
    */
    cb(null, './uploads');
  },
  filename: (req, file, cb) => {
    /*
      uuidv4() will generate a random ID that we'll use for the
      new filename. We use path.extname() to get
      the extension from the original file name and add that to the new
      generated ID. These combined will create the file name used
      to save the file on the server and will be available as
      req.file.pathname in the router handler.
    */
    const newFilename = `${uuidv4()}${path.extname(file.originalname)}`;
    cb(null, newFilename);
  },
});
```

2. use the package with multer and call it in the router 

```js
const upload = multer({ storage });

router.post('/', upload.single('selectedFile'), (req, res) => {
  /*
    We now have a new req.file object here. At this point the file has been saved
    and the req.file.filename value will be the name returned by the
    filename() function defined in the diskStorage configuration. Other form fields
    are available here in req.body.
  */
  res.send();
});
```

### Frontend

```js
import React, { Component } from 'react';
import axios from 'axios';

export default class UserForm extends Component {
  constructor() {
    super();
    this.state = {
      description: '',
      selectedFile: '',
    };
  }

  onChange = (e) => {
    switch (e.target.name) {
      case 'selectedFile':
        this.setState({ selectedFile: e.target.files[0] });
        break;
      default:
        this.setState({ [e.target.name]: e.target.value });
    }
  }

  onSubmit = (e) => {
    e.preventDefault();
    const { description, selectedFile } = this.state;
    let formData = new FormData();

    formData.append('description', description);
    formData.append('selectedFile', selectedFile);

    axios.post('/uploadFiles', formData)
      .then((result) => {
        // access results...
        console.log(result);
      });
  }

  render() {
    const { description, selectedFile } = this.state;
    return (
      <form onSubmit={this.onSubmit}>
        <input
          type="text"
          name="description"
          value={description}
          onChange={this.onChange}
        />
        <input
          type="file"
          name="selectedFile"
          onChange={this.onChange}
        />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```


# Reference

https://blog.stvmlbrn.com/2017/12/17/upload-files-using-react-to-node-express-server.html