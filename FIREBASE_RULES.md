# Firebase Security Rules

## Firestore Rules (For Production)

Replace the default rules in Firebase Console → Firestore Database → Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    
    // Users collection - users can only read/write their own data
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Patients collection - authenticated users can read/write
    match /patients/{patientId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update, delete: if request.auth != null && 
        (resource.data.doctorId == request.auth.uid || 
         get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin');
    }
    
    // Cases collection - authenticated users can read/write
    match /cases/{caseId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update, delete: if request.auth != null && 
        (resource.data.doctorId == request.auth.uid || 
         get(/databases/$(database)/documents/users/$(request.auth.uid)).data.role == 'admin');
    }

    // Admin Keys - allow doctors to check and claim keys
    match /admin_keys/{keyId} {
      allow read, update: if request.auth != null;
    }
  }
}
```

## Storage Rules (If you add file uploads later)

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.resource.size < 5 * 1024 * 1024;
    }
  }
}
```

## Notes

- **Test Mode**: For hackathon/development, you can use test mode (allows all reads/writes)
- **Production**: Use the rules above for production deployment
- **Admin Access**: Admins can read/write all data
- **Doctor Access**: Doctors can only modify their own patients/cases
