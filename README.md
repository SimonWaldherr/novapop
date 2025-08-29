# NovaPop

A sleek, accessible JavaScript library for creating beautiful popups, modals, tooltips, toasts, and lightboxes with zero dependencies.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-0.1.0-blue.svg)](https://github.com/SimonWaldherr/novapop)

## ✨ Features

- **🚫 Zero Dependencies** - Pure JavaScript, no external libraries required
- **♿ Accessible** - ARIA labels, focus management, keyboard navigation
- **🎨 Themeable** - Customizable via CSS variables
- **📱 Responsive** - Works seamlessly on mobile and desktop
- **🎵 Audio Support** - Built-in sound effects and custom audio URLs
- **⚡ Lightweight** - Under 35KB uncompressed
- **🌐 Universal** - AMD, CommonJS, and global support

### Component Types

- **Modals** - popup, confirm, prompt with rich form inputs
- **Lightbox** - Image and video galleries with navigation
- **Tooltips** - Smart positioning, interactive, delegated events
- **Toasts** - Success, error, warning, and info notifications
- **Queue** - Chain multiple modals in sequence
- **Audio** - Sound effects and volume controls

## 📦 Installation

### CDN
```html
<script src="https://cdn.jsdelivr.net/gh/SimonWaldherr/novapop/novapop.js"></script>
```

### Download
Download `novapop.js` and include it in your project:
```html
<script src="path/to/novapop.js"></script>
```

### Module Systems
```javascript
// CommonJS
const NovaPop = require('./novapop.js');

// AMD
define(['./novapop.js'], function(NovaPop) {
  // Use NovaPop
});

// ES6 (if using a bundler)
import NovaPop from './novapop.js';
```

## 🚀 Quick Start

### Basic Popup
```javascript
NovaPop.popup({
  title: 'Hello World',
  content: 'This is a simple popup!',
  buttons: [
    { label: 'Cancel', action: 'cancel' },
    { label: 'OK', action: 'ok', accent: true }
  ]
});
```

### Confirm Dialog
```javascript
const confirmed = await NovaPop.confirm({
  title: 'Delete file?',
  content: 'This action cannot be undone.',
  okText: 'Delete',
  danger: true
});

if (confirmed) {
  console.log('User confirmed deletion');
}
```

### Rich Prompt
```javascript
const data = await NovaPop.prompt({
  title: 'User Registration',
  inputs: [
    { type: 'text', name: 'name', label: 'Full Name', required: true },
    { type: 'email', name: 'email', label: 'Email', required: true },
    { type: 'select', name: 'role', label: 'Role', 
      options: [
        { label: 'User', value: 'user' },
        { label: 'Admin', value: 'admin' }
      ]
    }
  ],
  validate: (data) => {
    if (!data.name) return 'Name is required';
    if (!data.email.includes('@')) return 'Valid email required';
  }
});

console.log('Form data:', data);
```

### Toast Notifications
```javascript
// Success toast
NovaPop.toast({
  type: 'success',
  message: 'File saved successfully!',
  duration: 3000
});

// Toast with action button
NovaPop.toast({
  type: 'info',
  message: 'You have unsaved changes.',
  action: {
    label: 'Save now',
    onClick: () => saveDocument()
  }
});
```

### Tooltips
```javascript
// Basic tooltip
NovaPop.tooltip(document.getElementById('button'), {
  content: 'This is a helpful tooltip',
  placement: 'top'
});

// Interactive tooltip
NovaPop.tooltip(element, {
  content: 'Click me for more info',
  interactive: true,
  followCursor: true
});

// Delegated tooltips (for dynamic content)
NovaPop.tipDelegate(container, '.tooltip-target', {
  content: 'Shared tooltip configuration',
  placement: 'auto'
});
```

### Lightbox
```javascript
NovaPop.lightbox({
  items: [
    { src: 'image1.jpg', caption: 'Beautiful sunset' },
    { src: 'video.mp4', type: 'video', caption: 'Nature video' },
    { type: 'html', html: '<div>Custom HTML content</div>' }
  ]
});
```

## 🎛️ API Reference

### Popup Options
```javascript
NovaPop.popup({
  title: 'Modal Title',           // string
  content: 'Text content',        // string
  html: '<p>HTML content</p>',    // string (alternative to content)
  animation: 'fade',              // 'fade' | 'slide' | 'zoom'
  closeOnEsc: true,               // boolean
  closeOnBackdrop: true,          // boolean
  showCloseButton: true,          // boolean
  timer: 0,                       // auto-close timeout (ms)
  sound: 'beep',                  // string | object | null
  buttons: [                      // array of button objects
    {
      label: 'Button Text',
      action: 'custom',
      accent: true,               // boolean
      danger: false,              // boolean
      onClick: (result, api) => {}, // function
      keepOpen: false             // boolean
    }
  ],
  beforeClose: (result) => {},    // function (can return false to prevent)
  onClose: (result) => {},        // function
  onOpen: () => {}                // function
});
```

### Toast Types
- `success` - Green checkmark icon
- `error` - Red error icon  
- `warn` - Yellow warning icon
- `info` - Blue info icon

### Tooltip Placements
- `auto` - Smart auto-positioning
- `top`, `bottom`, `left`, `right`
- `top-start`, `top-end`, `bottom-start`, `bottom-end`

### Audio Options
```javascript
// Built-in sound
NovaPop.playSound('beep');

// Custom frequency
NovaPop.playSound({ freq: 440, duration: 0.2 });

// External URL
NovaPop.playSound('https://example.com/sound.mp3');

// Volume control
NovaPop.audio({ volume: 0.5, mute: false });
```

## 🎨 Theming

NovaPop uses CSS custom properties for easy theming:

```css
:root {
  --np-bg: #111;                    /* Modal background */
  --np-fg: #fff;                    /* Text color */
  --np-accent: #4f46e5;             /* Accent color */
  --np-backdrop: rgba(0,0,0,.6);    /* Overlay background */
  --np-radius: 14px;                /* Border radius */
  --np-shadow: 0 20px 40px rgba(0,0,0,.25); /* Box shadow */
  --np-tooltip-bg: #111;            /* Tooltip background */
  --np-toast-bg: #111;              /* Toast background */
  --np-danger: #ef4444;             /* Danger color */
  --np-success: #16a34a;            /* Success color */
  --np-warning: #f59e0b;            /* Warning color */
}
```

## 🌐 Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- iOS Safari 12+
- Android Chrome 60+

## 🎮 Demo

Open `demo.html` in your browser to see all features in action, or visit the [live demo](#) (if available).

The demo includes:
- Interactive examples of all components
- Theming showcase
- Audio controls
- Form validation examples
- Accessibility demonstrations

## 📚 Advanced Usage

### Queue Multiple Modals
```javascript
const results = await NovaPop.queue([
  { title: 'Step 1', content: 'First modal' },
  { title: 'Step 2', content: 'Second modal' },
  { title: 'Step 3', content: 'Final step' }
]);

console.log('All steps completed:', results);
```

### Custom Validation
```javascript
const userData = await NovaPop.prompt({
  title: 'Registration',
  inputs: [
    { type: 'password', name: 'password', label: 'Password' },
    { type: 'password', name: 'confirm', label: 'Confirm Password' }
  ],
  validate: (data) => {
    if (data.password !== data.confirm) {
      return 'Passwords do not match';
    }
    if (data.password.length < 8) {
      return 'Password must be at least 8 characters';
    }
  }
});
```

### Lifecycle Hooks
```javascript
const modal = NovaPop.popup({
  title: 'Loading...',
  content: 'Please wait...',
  onOpen: () => {
    console.log('Modal opened');
    // Start loading process
  },
  beforeClose: (result) => {
    // Return false to prevent closing
    return confirm('Are you sure you want to close?');
  },
  onClose: (result) => {
    console.log('Modal closed with:', result.action);
  }
});

// Programmatically close
setTimeout(() => {
  modal.close({ action: 'timeout' });
}, 5000);
```

## 🔧 Utility Functions

```javascript
// Close all open modals and toasts
NovaPop.destroyAll();

// Get library version
console.log(NovaPop.version); // "0.1.0"

// Manual tooltip control
NovaPop.tipShow(element, { content: 'Manual tooltip' });
NovaPop.tipHide();
```

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📧 Support

For questions, issues, or feature requests, please [open an issue](https://github.com/SimonWaldherr/novapop/issues) on GitHub.

---

Built with ❤️ by [Simon Waldherr](https://github.com/SimonWaldherr)