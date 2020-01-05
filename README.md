# React Camera Extended [![Travis status build](https://travis-ci.org/decabits/react-camera-extended.svg?branch=master)](https://travis-ci.org/decabits/react-camera-extended/) [![npm version](https://badge.fury.io/js/react-camera-extended.svg)](https://badge.fury.io/js/react-camera-extended)

Original Credits & Source Code From - [React Camera](https://github.com/Miniplop/react-camera)

Camera Module with ability to -

1. Take Photos.
2. Swap Camera Interface on Mobile Devices.

## Getting started

`npm install react-camera-extended`

or

`yarn add react-camera-extended`

## Usage

```
import Camera from 'react-camera-extended';
// Use ExifOrientationImg to make sure image does not rotate due to Exif Rotation
import ExifOrientationImg from 'react-exif-orientation-img';

export default class CameraInterface extends Component {

  constructor(props) {
    super(props);
    this.takePicture = this.takePicture;
  }

  componentDidMount() {
    this.state = {
      cameraState: 'open'
    }
  }

  takePicture = () => {
    this.camera.src = this.camera.capture();
    this.setState(({cameraState: 'preview'}));
  };

  render() {
    if (this.state.cameraState ==- 'preview') {
      return(
        <div>
          <ExifOrientationImg className="camera-preview__image" src={this.props.src}/>
        </div>
      )
    } else {
      return (
        <div className="camera-interface">
          <Camera ref={(cam) => { this.camera = cam;}} tryRearCamera={true} />
          <footer className="camera-interface__footer" >
            <img src={RecordIcon}  className="camera-interface__footer__capture-button" onClick={this.takePicture} >
            </img>
          </footer>
        </div>
      );
    }
  }
}
```

## Available Props

- `video` - true if you just need any video source from device. You can set preference by referring [here](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia).
- `audio` - true|false. False by default as we currently only support capture photo.
- `styles` - To override default style use this prop. Default values -

  ```
  {
    video: {
      minWidth: '100%',
      minHeight: '100%',
      width: 'auto',
      height: 'auto',
      position: 'absolute',
      top: 0,
      left: 0
    },
    videoContainer: {
      position: 'absolute',
      top: 0,
      bottom: 0,
      width: '100%',
      height: '100%',
      overflow: 'hidden'
    }
  }
  ```

- `tryRearCamera` - Set true if you intend to use this in mobile phone and want rear camera to load by default. Default - false

## Methods

Make sure to set camera reference like given in the example. Once you have `this.camera = ref`, you can use following methods -

- `this.camera.capture()` - Captures the and returns image in data url format.
- `this.camera.setVideoStream(tryRearCamera = true|false)` - Call this to toggle between front and rear camera.

## Contribution

Please fork the repository and open the pull request against master. Feel free to reach out to us at [info@decabits.com](mailto:info@decabits.com)
