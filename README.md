# ra-appwrite

[![Stable Release](https://img.shields.io/npm/v/ra-appwrite)](https://www.npmjs.com/package/ra-appwrite)
![License](https://img.shields.io/github/license/g33kdev/ra-appwrite.svg?style=flat-square)

This package provides a Data Provider and Auth Provider to integrate [Appwrite](https://appwrite.io/) with [react-admin](https://marmelab.com/react-admin).

The Data Provider supports:

- Documents

The Auth Provider supports:

- Login
- Logout
- Permissions (Teams)

## Installation

```sh
yarn add ra-appwrite
# or
npm install ra-appwrite
```

## Usage

```jsx
import { Client, Account } from 'appwrite'
import {
	appWriteDataProvider,
	appWriteAuthProvider,
	LoginForm,
} from 'ra-appwrite'
import {
	Admin,
	EditGuesser,
	ListGuesser,
	Resource,
	ShowGuesser,
	Login,
} from 'react-admin'

// Initialize Appwrite client
const client = new Client()
client
	.setEndpoint(APPWRITE_ENDPOINT) // often https://cloud.appwrite.io/v1
	.setProject(APPWRITE_PROJECTID)

// Initialize the providers
const dataProvider = appWriteDataProvider({
	client,
	databaseId: APPWRITE_DATABASEID,
	collectionIds: {
		contacts: APPWRITE_COLLECTIONID_CONTACTS,
		companies: APPWRITE_COLLECTIONID_COMPANIES,
	},
})

const account = new Account(client)
const authProvider = appWriteAuthProvider({ client, account })

// custom login page with email and password instead of username and password
const LoginPage = () => (
	<Login>
		<LoginForm />
	</Login>
)

const App = (): JSX.Element => (
	<Admin
		dataProvider={dataProvider}
		authProvider={authProvider}
		loginPage={LoginPage}
	>
		{/* the resource names must match the collection IDs */}
		<Resource
			name='contacts'
			list={ListGuesser}
			edit={EditGuesser}
			show={ShowGuesser}
		/>
		<Resource
			name='companies'
			list={ListGuesser}
			edit={EditGuesser}
			show={ShowGuesser}
		/>
	</Admin>
)

export default App
```

## Roadmap

- Add support for fetching teams
- Add support for fetching files
