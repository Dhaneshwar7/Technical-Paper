# Technical-Paper
These are my Learning Notes of All Technologies in different .MD files


### Go To Section (Chetsheets) :-
1.[React Router](#React-Router-Cheatsheet)
&nbsp; 2.[Firebase Cheatsheet](#firebase-cheatsheet)
&nbsp; 3.[React Context API](#react-context-api)
&nbsp; 4.[React Flat Folder Structure](#react-flat-folder-structure)
&nbsp; 5.[React Redux](#react-redux)
&nbsp; 6.[Redux Persist](#redux-persist)
&nbsp; 7.[Netlify](#netlify)
&nbsp; 7.[Netlify](#netlify)
&nbsp; 7.[Stripe with React js](#stripe-with-react-js)
&nbsp; 7.[Testing](#testing-code-wookay)

# ----------------------- React Router Cheatsheet ------------------
<div align="center">
<img src="images/ReactRouter.png" width="300" height="150" /> 	
</div>

## Some Reading Notes 

[Official Website React Router 🔗](https://reactrouter.com/en/main)

### React Router 
React Router is a collection of navigational components within your application. With the latest version, React Router v6, there are several new features and improvements over the previous versions. This article will help you understand how to use React Router in a modern React application.

# Where i was Stuck & Solution(R&D) & Learning

>[!NOTE]
>        - Browser Router Structure

`This is /main.tsx`
```js
import { BrowserRouter } from 'react-router-dom';

<BrowserRouter>
     <App />
</BrowserRouter>
```
`This is App.tsx`
```js
import { Route, Routes } from 'react-router-dom';

<Routes>
        <Route path="/" element={<MainLayout />}>
            <Route index element={<HomePage />} />
            <Route path="/shop/*" element={<ShopLayout />}>
                <Route path="all-products" element={<AllProducts />} />
                <Route path=":categoryName" element={<CategoryPreview />} />
            </Route>
            <Route path="/shop/cart-checkout" element={<CartCheckoutPage />} />
            <Route path="/authentication" element={<AuthenticationPage />} />
        </Route>
</Routes>
```


Reading Documentation And Took help of ChatGPT to undestand more
>[Firebase Rules Documentaion]([https://firebase.google.com/docs/firestore/security/get-started?hl=en&authuser=0](https://reactrouter.com/en/main))
>[Structure Data in Firestore]([https://firebase.google.com/docs/firestore/manage-data/structure-data?hl=en&authuser=0](https://reactrouter.com/en/main))


## 𖦋 -> React Router Structure Diagram:-

This is React Router \*For Learning Purpose i created\* 
```mermaid
graph TD;
BrowserRouter-->App;
App-->Routes;
Routes-->Route;
Route-->/Home;
Route-->/Authenticaton;
Route-->/AboutUs;
Route-->/ContactUs;
Route-->/Shop;
Route-->/Cart;
Route-->/CartChekout;
```
## 𖦋 -> Basic Components and Hooks of React Router Which i Used in Task :-

####      * `<Link>`: - A <Link> is an element that lets the user navigate to another page by clicking or tapping on it. In react-router-dom.
```js
import { Link } from "react-router-dom";
const navLinks=[{id:1,link:'/home'},{id:2,link:'/about'},{id:3,link:'/contactus'},{id:4,link:'/auth'}]

function NavigationBar() {
  return (
    <div>
          <span>Logo</span>
          <ul>
               {navLinks.map(nav => (
                    <li key={nav.id}>
                         <Link to={`/${nav.link}`}>{nav?.link.toUpperCase()}</Link>
                    </li>))}
          </ul>
    </div>
  );
}
```
####      * `<NavLink>`: - A <NavLink> is a special kind of <Link> that knows whether or not it is "active", "pending", or "transitioning". 
```js
import { NavLink } from "react-router-dom";
<NavLink
  to="/messages"  className={({ isActive, isPending }) => isPending ? "pending" : isActive ? "active" : ""}>
  Messages
</NavLink>;
```
####      * `<Outlet>`: - An <Outlet> should be used in parent route elements to render their child route elements. This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route.

```js
import { Outlet } from 'react-router-dom';
function MainLayout() {
  return (
    <>
     <Header/>
      <Outlet />
     <Footer/>
    </>
  )};

function App() {
  return (
    <Routes>
      <Route path="/" element={<MainLayout />}>
        <Route
          index
          element={<HomePage />}
        />
        <Route path="aboutus" element={<AboutUs />} />
        <Route path="contactus" element={<ContactUs />} />
...etc
      </Route>
    </Routes>
  );
}
```
####      * `<useNavigate>`: - The useNavigate hook returns a function that lets you navigate programmatically, for example in an effect:
```js
import { useNavigate } from "react-router-dom";
const navigate = useNavigate();

const hancleGoogleSignIn = async () => {
     try {
          const { user } = await asyncSignInWithGoogle();
			if (user) {
				await asyncCurrentLoggedInUser();
				navigate('/');
			}
		} catch (error) {
			console.error(error);
     }};
```


# ------------------ Firebase CheatSheet ---------------
<div align="center">
<img src="images/fibase.svg" width="200" height="200" /> 	
</div>

# Firebase Technical Paper
## Some Reading Notes 

### Authentication:-
Firebase Authentication provides backend services to help authenticate users in your app. It supports various authentication methods, including email/password and OAuth providers like Google and Facebook.
### Firestore:-
Firestore is a flexible, scalable database for mobile, web, and server development. It provides real-time synchronization and offline support, making it easy to build responsive applications.
### Storage:-
Firebase Storage provides secure file uploads and downloads for Firebase apps. It is designed to scale from petabytes to exabytes, and to handle high-frequency use cases like streaming and uploading media.
### Firebase Hosting:-
is a fully-managed hosting service for static and dynamic content as well as microservices. It provides fast and secure hosting with features such as SSL, custom domains, and auto-scaling.

# Where i was Stuck & Solution(R&D) & Learning

>[!WARNING]
>        - In Firebase CRUD OPERATIONS Access Change Rules Section.
>[!TIP]
> Like This can Manipulate Operations. 
```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
    allow create: if request.auth !=null && request.auth.uid == request.resource.data.userId;
    allow update,delete :  if request.auth != null ;
    allow read: if true;
    }
  }
}
```
Reading Documentation And Took help of ChatGPT to undestand more
>[Firebase Rules Documentaion](https://firebase.google.com/docs/firestore/security/get-started?hl=en&authuser=0)
>[Structure Data in Firestore](https://firebase.google.com/docs/firestore/manage-data/structure-data?hl=en&authuser=0)


# 𖦋 -> Firebase Structure Diagram:-

This is Firebase Structure \*For Learning Purpose i created\* 
```mermaid
graph TD;
Firebase-->Authentication;
Authentication-->Sign_In_Methods;
Sign_In_Methods-->Native_Providers-->Email_Password/Phone-->User/User_Detail/Token;
Sign_In_Methods-->Additional_Providers-->Google/Facebook/Apple/Microsoft/Github-->User/User_Detail/Token;

Firebase_Database/Storage-->

Data-->Start_Collection1-->Products;
Products-->Add_Document;
Add_Document-->Hats;
Add_Document-->Jackets;
Add_Document-->Sneakers;
Hats-->Items_Array;
Jackets-->Items_Array;
Sneakers-->Items_Array;
Items_Array-->Object_Id_ImageUrl_Name_Price;

Firebase-->Firebase_Database/Storage-->Rules-->Permissions_Code;



Data-->Start_Collection2-->Cart;
Cart-->Add_Documents;
Add_Documents-->Cart_Items;
Add_Documents-->Cart_Count;
Add_Documents-->Cart_Total;
Cart_Items-->Array;
Cart_Count-->Number;
Cart_Total-->Number;
Firebase-->Hosting-->Firebase_Login;
Hosting-->Firebase_init;
Hosting-->Firebase_deploy;
```

# 1️⃣-> Authentication Firebase Setup with Firestore Database

#### Setup Code Provided from Firebase after Creating Project/App

`./firebase.ts`
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

## Authentication Actions

### Imports ⇣
`./FirebaseAuthActions.ts`
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
> This is Firebase *onAuthStateChanged method for fetch Logged in user !!
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
### * SignInUserWithEmailAndPassword
> This just take Auth as Parameter and  Signout --> Logged in User !!
```js
export const asyncLogOutUser = async () => {
	return await signOut(auth);
};
```
# 2️⃣-> Firestore Database
`/FirebaseBooksAction.ts`
```js
/*  -----------Books Actions--------- */
export const asynchandleBookFormSubmit = async bookData => {
	const allBooksCollection = collection(db, 'books');
	try {
		if (!bookData.bookName == '' || !bookData.publishDate == '') {
			return await addDoc(allBooksCollection, bookData);
		}
	} catch (error) {console.error(error)}
};

export const asyncGetBooksData = async () => {
	const allBooksCollection = collection(db, 'books');
	try {
		const data = await getDocs(allBooksCollection);
		return data.docs.map(doc => ({...doc.data(),id: doc.id,}));
	} catch (error) {console.error(error)}};

export const asyncHandleEditBook = async (bookId, editedBookName) => {
	try {
		const bookDoc = await doc(db, 'books', bookId);
		return await updateDoc(bookDoc, { title: editedBookName });
	} catch (error) {console.error(error)}};

export const asyncHandleDeleteBook = async bookId => {
	try {
		const bookDoc = doc(db, 'books', bookId);
		await deleteDoc(bookDoc);
	} catch (error) {console.error(error)}};

export const handleUploadFile = async () => {
	if (!uploadFile) return null;
	const fileFolderRef = ref(storage, `booksImages/${uploadFile.name}`);
	try {
		await uploadBytes(fileFolderRef, uploadFile);
	} catch (error) {console.error(error)}};
```
# 3️⃣-> Hosting
>Fire base also Provide Hosting Website/App
For that, After Completing Ourt Project we have to Execute :-
```js
npm run build
```
Which will Generate `dist` || `build` Folder for Deployement where our final `index.html` Presents
Then we have to Setup Hosting Project Procedure which will get from Firebase Hosting Tab ,
There need to some Action like --
`\* First Command for Setup your Firebase Email Id *\`
```js

firebase login
```
There Are the Commands helps if stuck in Login/CLI Setup
`With Firebase CLI you can have multiple accounts logged in.

>Using firebase `login:add` will login another account.

>Using firebase `login:list` will list logged accounts.

>Using firebase `login:use` will set default account for current project directory.`

>And you can use `firebase logout` to logout from Firebase.

🔗 [Reference Link For Reading Login Setup in Terminal](https://stackoverflow.com/questions/75563709/how-could-i-change-my-firebase-login-account-to-another-account-and-login-again)

### -------- Resting Code WoOkay ------- 

Next Command is 
```js
firebase init
```
Which will Come-Up with so Many Question like this ;;- Proceed Accordigly-
```js
//Before firebase init make sure that run Build command like 
npm run build
//this after completion this will provide dist/build folder put that name in this line of code 
? What do you want to use as your public directory? Dist
? Configure as a single-page app (rewrite all urls to /index.html)? No
? Set up automatic builds and deploys with GitHub? Yes
✔  Wrote dist/404.html
? File dist/index.html already exists. Overwrite? No
? For which GitHub repository would you like to set up a GitHub workflow? (format: user/repository) Dhaneshwar7/Firebase-Learn
? Set up the workflow to run a build script before every deploy? No
? Set up automatic deployment to your site's live channel when a PR is merged? Yes
? What is the name of the GitHub branch associated with your site's live channel? Main
? The GitHub workflow file for deploying to the live channel already exists. Overwrite?
firebase-hosting-merge.yml No

Final command –  firebase deploy
Hosting URL: https://fir-learn-hk.web.app
```
Done Almost Afte That Last Step 📍
```js
firebase deploy
```



