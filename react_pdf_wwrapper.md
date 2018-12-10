# React-PdfJs-Wrapper

## Wrapper 

```
/**
 * @class ReactPdfJs
 */
import PdfJsLib from 'pdfjs-dist';
import PropTypes from 'prop-types';
import React, { Component } from 'react';

export default class ReactPdfJs extends Component {
  static propTypes = {
    file: PropTypes.string.isRequired,
    page: PropTypes.number,
    onDocumentComplete: PropTypes.func,
  }

  static defaultProps = {
    page: 1,
    onDocumentComplete: null,
  }

  state = {
    pdf: null,
  };

  componentDidMount() {
    PdfJsLib.GlobalWorkerOptions.workerSrc = '//cdnjs.cloudflare.com/ajax/libs/pdf.js/2.0.550/pdf.worker.js';
    PdfJsLib.getDocument(this.props.file).then((pdf) => {
      this.setState({ pdf });
      if (this.props.onDocumentComplete) {
        this.props.onDocumentComplete(pdf.pdfInfo.numPages);
      }
      pdf.getPage(this.props.page).then((page) => {
        const scale = 1.5;
        const viewport = page.getViewport(scale);

        const { canvas } = this;
        const canvasContext = canvas.getContext('2d');
        canvas.height = viewport.height;
        canvas.width = viewport.width;

        const renderContext = {
          canvasContext,
          viewport,
        };
        page.render(renderContext);
      });
    });
  }

  componentWillReceiveProps(newProps) {
    if (newProps.page !== this.props.page) {
      this.state.pdf.getPage(newProps.page).then((page) => {
        const scale = 1.5;
        const viewport = page.getViewport(scale);

        const { canvas } = this;
        const canvasContext = canvas.getContext('2d');
        canvas.height = viewport.height;
        canvas.width = viewport.width;

        const renderContext = {
          canvasContext,
          viewport,
        };
        page.render(renderContext);
      });
    }
  }

  render() {
    return <canvas ref={(canvas) => { this.canvas = canvas; }} />;
  }
}
```

## Usage


```
import React, { Component } from 'react';
import Pdf from './ReactPdfJs';

export default class App extends Component {
  state = { page: 1 };

  onDocumentComplete = (pages) => {
    this.setState({ page: 1, pages });
  }

  handlePrevious = () => {
    this.setState({ page: this.state.page - 1 });
  }

  handleNext = () => {
    this.setState({ page: this.state.page + 1 });
  }

  renderPagination = (page, pages) => {
    let previousButton = (
      <li className="previous">
        <button onClick={this.handlePrevious} className="btn btn-link">
          Previous
        </button>
      </li>
    );
    if (page === 1) {
      previousButton = (
        <li className="previous disabled">
          <button className="btn btn-link">
            Previous
          </button>
        </li>
      );
    }
    let nextButton = (
      <li className="next">
        <button onClick={this.handleNext} className="btn btn-link">
          Next
        </button>
      </li>
    );
    if (page === pages) {
      nextButton = (
        <li className="next disabled">
          <button className="btn btn-link">
            Next
          </button>
        </li>
      );
    }
    return (
      <nav>
        <ul className="pager">
          {previousButton}
          {nextButton}
        </ul>
      </nav>
    );
  }

  render () {
    let pagination = null;
    if (this.state.pages) {
      pagination = this.renderPagination(this.state.page, this.state.pages);
    }
    return (
      <div>
        <Pdf file="compressed.tracemonkey-pldi-09.pdf" onDocumentComplete={this.onDocumentComplete} page={this.state.page} />
        {pagination}
      </div>
    );
  }
}
```



## Reference

https://github.com/mikecousins/react-pdf-js
https://mozilla.github.io/pdf.js/examples/
