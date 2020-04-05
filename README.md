# HidroAdmin
A Vue.js 2 admin app, based on vue-admin, using vuex, vuexfire, vue-router and Firebase as the backend.

This project aims to be a template for using Firebase as a backend, and vue-admin as a frontend.

### Current features developed:

- Vuexfire for Firebase integration
- Firebase auth
- Ability to set a password (including Firebase reauth flow handling)
- Ability to link multiple auth providers
- Frontend Notification dispatching system (ie. not integrated with Cloud Messaging) and default notifications
- Protected Routes
- A User dashboard
- A basic User Notes taking feature, where completed / incompleted notes are shown on the User dashboard. Along with new note form that accepts a title, and wysiwyg body field (Quill)

### Installation

**NOTE: This app assumes you have a working Firebase instance with at least one of the auth providers; Google, Facebook, Github or Password enabled.**

1. Update `config/firebase.env.js` with your firebase config variables
2. `npm install`
3. `npm run dev`

### Firebase Rules
This app requires the following firebase rules (for notes facility)

``````
{
  "rules": {
    // ".read": true,
    // ".write": false,
    "users": {
      ".indexOn": "ID",
      "$uid": {
        ".validate": "$uid === auth.uid",
        // grants write access to the owner of this user account
        // whose uid must exactly match the key ($uid)
        ".write": "$uid === auth.uid",
        ".read": "auth != null && auth.uid == $uid"
      }
    },
    "notes": {
      ".indexOn": "uid",
        ".read" : "data.child(auth.uid).exists()",
      "$uid": {
        ".write": "$uid == auth.uid",
      }
    }
  }
}
``````

### WARNING !!!

THIS APP **SETS** FIREBASE REFS `/users` AND `/notes` !!!!

If you already have data at these refs, be sure to change the ref names in the file `/client/firebase-setup/ref-types.js`.  Otherwise, it will most likely be overwritten.

### Additional work

I have a companion node.js server app that runs on heroku.  It watches the firebase database and performs database actions using firebase-admin sdk.

I will aim to make this app publicly available too, but optional (ie. not required for vuexfire-admin to work).

---
### Credits

This project is inspired or powered by these people or projects so I want to thank them

- [Vue](https://github.com/vuejs/vue) great work
- [Bulma](https://github.com/jgthms/bulma) A modern CSS framework based on Flexbox
- [vue-admin](https://github.com/vue-bulma/vue-admin) for laying the foundations
- [VuexFire](https://github.com/posva/vuexfire) for work integrating Vuex & Firebase
- [vee-validate](https://github.com/baianat/vee-validate) for making form validation in Vue so easy
- [Firebase](https://firebase.google.com/)

#### MIT License
```
Copyright (c) 2018 Asociatia de Dezbateri Cantemir

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
