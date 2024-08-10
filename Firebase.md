# Firebase Technical Paper

## Authentication Firebase Setup

#### Setup Code Provided from Firebase after Creating Project/App

```js
import { initializeApp } from 'firebase/app';
import { getAnalytics } from 'firebase/analytics';
import { getAuth, GoogleAuthProvider } from 'firebase/auth';
import { getFirestore } from 'firebase/firestore';
const firebaseConfig = {
	apiKey: 'xxxxCopy-Paste-from-Firebase-xxxxx',
	authDomain: 'xxx-Project-Domain---xxxx.firebaseapp.com',
	projectId: 'xxxx-domain---',
	storageBucket: 'xxxx-domain---.appspot.com',
	messagingSenderId: 'xxx-Number---xxxx',
	appId: 'x:xxxx--AppId------xxx',
	measurementId: 'xxxxx--some--Id',
};
const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const googleProvider = new GoogleAuthProvider();
export const db = getFirestore(app);
const analytics = getAnalytics(app);

```
## Some Reading Notes 

### Authentication:-
Firebase Authentication provides backend services to help authenticate users in your app. It supports various authentication methods, including email/password and OAuth providers like Google and Facebook.
### Firestore:-
Firestore is a flexible, scalable database for mobile, web, and server development. It provides real-time synchronization and offline support, making it easy to build responsive applications.
### Storage:-
Firebase Storage provides secure file uploads and downloads for Firebase apps. It is designed to scale from petabytes to exabytes, and to handle high-frequency use cases like streaming and uploading media.
### Firebase Hosting:-
is a fully-managed hosting service for static and dynamic content as well as microservices. It provides fast and secure hosting with features such as SSL, custom domains, and auto-scaling.

# Authentication Actions

### Imports
```js
import {
	createUserWithEmailAndPassword,
	onAuthStateChanged,
	signInWithEmailAndPassword,
	signInWithPopup,
	signOut,
} from 'firebase/auth';
import { auth, googleProvider } from './Firebase';
```
### * SignInWithGoogle
```js
export const asyncSignInWithGoogle = async () => {
	return await signInWithPopup(auth, googleProvider);
};
/* Example How to use All Actions Where we Want --Changes is required as per Actions  */

// THIS IS FUNCION
const hancleGoogleSignIn = async () => {
		try {
			const { user } = await asyncSignInWithGoogle();
			// 	console.log(user);
			if (user) {
				await asyncCurrentLoggedInUser();
				setCurrentUser(user);
				navigate('/');
			}
		} catch (error) {
			console.error(error);
		}
	};

//THIS IS UI
<Button onClick={hancleGoogleSignIn}> Continue with Google </Button>
```
### * createUserWithEmailAndPassword 
> This take a <b> Auth, Email, Password </b> as Parameters and Create new Account of User in FireStore
```js
export const asyncCreateUserWithEmailAndPassword = async (email: string, password: string) => {
	return await createUserWithEmailAndPassword(auth, email, password);
};
```
### * SignInUserWithEmailAndPassword
> This also takes a <b> Auth, Email, Password </b> as Parameters and Sign In Successful !!
```js
export const asyncSignInUserWithEmailAndPassword = async (email: string,password: string) => {
	return  signInWithEmailAndPassword(auth, email, password);
};
```
### * onAuthStateChanged || This method check for current User if Logged In Or Not 
> This also takes a <b> Auth, Email, Password </b> as Parameters and Sign In Successful !!
```js
import {onAuthStateChanged} from 'firebase/auth';
export const asyncCurrentLoggedInUser = () => {
	return new Promise((resolve, reject) => {
		onAuthStateChanged(auth,user => {
				if (user) {
					resolve(user);
				} else {
					resolve(null);
				}
			},
			reject
		);});};
```



