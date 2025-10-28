# Sunrise Territory Village - CCR Compliance Review Checklist

A professional web-based form for conducting property compliance reviews, built with Firebase backend for data storage and management.

![Form Preview](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)
![Firebase](https://img.shields.io/badge/Firebase-v10.7.1-orange)

---

## 📋 Overview

This digital compliance checklist replaces the traditional PDF-based review process with a modern, user-friendly web form that:
- Automatically saves all submissions to Firebase Firestore
- Resets after each submission for quick multiple reviews
- Works on any device (desktop, tablet, mobile)
- Provides instant confirmation of successful submissions
- Stores data securely in the cloud

---

## ✨ Features

### Form Capabilities
- ✅ **26 Inspection Categories** covering all property aspects
- ✅ **4-Point Rating System** (Accept, Minor, Major, N/A)
- ✅ **Detailed Comments Section** for violation specifics
- ✅ **Follow-up Tracking** with dates and compliance status
- ✅ **Auto-Reset** after submission for efficiency
- ✅ **Mobile Responsive** design for on-site inspections
- ✅ **Professional Styling** matching HOA standards

### Inspection Categories
1. Overall Property Appearance
2. Exterior Structures (6 items)
3. Hardscape (2 items)
4. Landscaping (6 items)
5. Fixtures & Amenities (4 items)
6. Storage & Cleanliness (3 items)
7. Vehicles & Parking (3 items)

### Technical Features
- 🔥 **Firebase Firestore** backend
- 📱 **Progressive Web Design**
- 🔒 **Secure Data Storage**
- ⚡ **Real-time Validation**
- 📊 **Easy Data Export** (CSV/JSON)
- 🎨 **Custom Gradient Header**
- ✉️ **Success/Error Notifications**

---

## 🚀 Quick Start

### Prerequisites
- A Firebase account (free tier works perfectly)
- A domain or hosting service (multiple free options available)
- A text editor (VS Code, Notepad++, etc.)

### Setup Time
**Total: ~10 minutes**

---

## 📦 Installation

### Step 1: Clone or Download

```bash
# Clone the repository
git clone https://github.com/yourusername/ccr-compliance-form.git

# Or download the ZIP and extract it
```

### Step 2: Firebase Setup

1. **Create Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Click "Add project"
   - Name it: `sunrise-ccr-compliance`
   - Disable Google Analytics (optional)
   - Click "Create project"

2. **Enable Firestore Database**
   - Click "Firestore Database" in left menu
   - Click "Create database"
   - Select "Start in production mode"
   - Choose your location
   - Click "Enable"

3. **Configure Security Rules**
   - Go to Firestore → Rules tab
   - Replace with:
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /complianceReviews/{document=**} {
         allow create: if true;
         allow read, update, delete: if request.auth != null;
       }
     }
   }
   ```
   - Click "Publish"

4. **Get Firebase Config**
   - Click ⚙️ → Project settings
   - Scroll to "Your apps"
   - Click web icon `</>`
   - Register app as "CCR Form"
   - Copy the `firebaseConfig` object

5. **Update HTML File**
   - Open `index.html` in your text editor
   - Find this section (around line 1300):
   ```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT_ID.appspot.com",
       messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
   ```
   - Replace with your actual Firebase config
   - Save the file

### Step 3: Deploy (Choose One Method)

#### Option A: Netlify (Easiest)
1. Create folder named `ccr-form`
2. Put `index.html` inside (rename your file to `index.html`)
3. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
4. Drag folder to upload
5. Done! Get instant URL

#### Option B: GitHub Pages
1. Create GitHub repository
2. Upload `index.html`
3. Go to Settings → Pages
4. Enable Pages
5. Live at `https://yourusername.github.io/repository-name`

#### Option C: Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy --only hosting
```

#### Option D: Vercel
1. Go to [vercel.com](https://vercel.com)
2. Sign up with GitHub
3. Import project
4. Deploy

---

## 🎯 Usage

### For Review Team Members

1. **Access the Form**
   - Open the hosted URL
   - Works on any device

2. **Fill Out Review**
   - Enter date, team names, and property address
   - Rate each inspection item (Accept/Minor/Major/N/A)
   - Add detailed comments if violations found
   - Complete follow-up section

3. **Submit**
   - Click "Submit" button
   - See success confirmation
   - Form automatically resets for next review

### For Administrators

1. **View Submissions**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Select your project
   - Click "Firestore Database"
   - View "complianceReviews" collection

2. **Export Data**
   - Click on a submission
   - Click ⋮ menu → "Export"
   - Choose CSV or JSON format

3. **Search/Filter**
   - Use Firestore filters
   - Filter by date, address, or status

---

## 📊 Data Structure

Each submission creates a document in Firestore with this structure:

```javascript
{
  // Basic Information
  date: "2025-10-27",
  reviewTeam: "John Smith, Jane Doe",
  propertyAddress: "123 Main St",
  
  // Inspection Results (sample)
  overallAppearance: "accept",
  paintStucco: "minor",
  tileRoof: "accept",
  // ... (all other fields)
  
  // Comments & Follow-up
  detailedComments: "Front paint needs touch-up near garage",
  violationNotice: "yes",
  violationNoticeDate: "2025-10-27",
  complianceDeadline: "2025-11-15",
  reinspectionDate: "2025-11-16",
  complianceStatus: "in-progress",
  
  // System Fields
  submittedAt: "2025-10-27T14:30:00.000Z"
}
```

---

## 🎨 Customization

### Change Color Theme

Edit the CSS gradient in `index.html`:

```css
/* Current: Purple gradient */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Blue theme */
background: linear-gradient(135deg, #2196F3 0%, #1976D2 100%);

/* Green theme */
background: linear-gradient(135deg, #4CAF50 0%, #388E3C 100%);

/* Orange theme */
background: linear-gradient(135deg, #FF9800 0%, #F57C00 100%);
```

### Add Your Logo

In the header section, add:

```html
<div class="form-header">
    <img src="your-logo.png" alt="Logo" style="max-width: 200px; margin-bottom: 16px;">
    <h1 class="form-title">Sunrise Territory Village<br>CCR Compliance Review Checklist</h1>
    ...
</div>
```

### Modify Form Fields

To add/remove/edit inspection items, find the relevant section in the HTML and modify the structure:

```html
<div class="question">
    <div class="item-label">Your new inspection item</div>
    <div class="radio-group">
        <!-- Radio buttons here -->
    </div>
</div>
```

---

## 🔒 Security

### Current Setup
- ✅ Anyone can submit forms (public)
- ✅ Only authenticated users can view/edit/delete (admin)

### To Restrict Submissions

Update Firestore rules to require authentication:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /complianceReviews/{document=**} {
      allow create: if request.auth != null;  // Changed from: if true
      allow read, update, delete: if request.auth != null;
    }
  }
}
```

Then add Firebase Authentication to your HTML.

---

## 📱 Browser Support

- ✅ Chrome (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

---

## 💰 Costs

### Firebase Free Tier (Spark Plan)
- **Firestore**: 1GB storage, 50K reads/day, 20K writes/day
- **Hosting**: 10GB storage, 360MB/day transfer
- **Cost for this form**: **$0/month** (unless you get millions of submissions)

### Hosting Costs
All recommended hosting options have generous free tiers:
- Netlify: 100GB bandwidth/month
- GitHub Pages: Unlimited
- Vercel: 100GB bandwidth/month
- Firebase Hosting: 360MB/day

**Expected cost: $0** ✅

---

## 🛠️ Troubleshooting

### Form Won't Submit
1. Open browser console (F12)
2. Check for error messages
3. Verify Firebase config is correct
4. Check Firestore security rules

### "Permission Denied" Error
- Update Firestore security rules
- Ensure Firestore is enabled
- Check Firebase config

### Data Not Appearing in Firestore
- Verify you're looking at correct project
- Check "complianceReviews" collection
- Wait a few seconds and refresh

### Form Not Resetting
- Check browser console for JavaScript errors
- Ensure Firebase SDK is loading correctly
- Try clearing browser cache

---

## 📝 Future Enhancements

Potential features to add:
- [ ] Photo upload capability
- [ ] Email notifications on submission
- [ ] Admin dashboard for viewing submissions
- [ ] Export to PDF
- [ ] Multi-language support
- [ ] Offline mode
- [ ] Digital signatures
- [ ] Automated violation letters

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Support

### Documentation
- [Firebase Setup Guide](Firebase_Setup_Instructions.md)
- [Custom Domain Setup](#configure-custom-domain)

### Contact
- **Email**: board@sunriseterritory.com
- **Issues**: [GitHub Issues](https://github.com/yourusername/ccr-compliance-form/issues)

---

## 🙏 Acknowledgments

- Built for Sunrise Territory Village Board of Directors
- Powered by [Firebase](https://firebase.google.com/)
- Inspired by modern form design principles
- Special thanks to the review team for their feedback

---

## 📈 Version History

### v1.0.0 (2025-10-27)
- ✨ Initial release
- ✅ All 26 inspection categories
- ✅ Firebase integration
- ✅ Auto-reset functionality
- ✅ Mobile responsive design
- ✅ Success/error notifications

---

## 🔗 Quick Links

- [Live Demo](https://your-form-url.web.app)
- [Firebase Console](https://console.firebase.google.com/)
- [Report Bug](https://github.com/yourusername/ccr-compliance-form/issues)
- [Request Feature](https://github.com/yourusername/ccr-compliance-form/issues)

---

**Made with ❤️ for Sunrise Territory Village**

*Last Updated: October 27, 2025*
