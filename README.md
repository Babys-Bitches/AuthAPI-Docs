# AuthAPI-Docs


***CONFIG SETUP***

**These settings has to be included in your project. In this example we are using axios wich can be installed with `npm install axios`**

```java
const axios = require('axios');

const VUE_APP_ENDPOINT = 'https://yourapi.domain.com:port'; // Your backend endpoint
const token = 'your_auth_token'; // Your authentication token
const appId = 'your_app_id'; // Your application ID
```

&nbsp;

***Generating License Keys***

**To generate license keys, you would typically use the generateLicenses function.**

```java
const generateLicense = async (duration, quantity) => {
    try {
        const response = await axios.post(`${VUE_APP_ENDPOINT}/backend/dashboard/api/v1/apps/${appId}/licenses`, {
            duration,
            quantity
        }, {
            headers: {
                'Content-Type': 'application/json',
                'authorization': token
            }
        });
        console.log('License generated:', response.data);
    } catch (error) {
        console.error('Error generating license:', error);
    }
};

generateLicense('30', '1'); // Example usage
```

&nbsp;

***Deleting License Keys***

**To delete a license key, the deleteLicense function.**

```java
const deleteLicense = async (licenseId) => {
    try {
        const response = await axios.delete(`${VUE_APP_ENDPOINT}/backend/dashboard/api/v1/apps/${appId}/licenses/${licenseId}`, {
            headers: {
                'Content-Type': 'application/json',
                'authorization': token
            }
        });
        console.log('License deleted:', response.data);
    } catch (error) {
        console.error('Error deleting license:', error);
    }
};

deleteLicense('license_id_here'); // Replace 'license_id_here' with your actual license ID
```

&nbsp;

***Resetting HWID on License Keys***

**To reset the HWID on license keys, the resetHWID function is used.**

```java
const resetHWID = async (licenseId) => {
    try {
        const response = await axios.put(`${VUE_APP_ENDPOINT}/backend/dashboard/api/v1/apps/${appId}/licenses/${licenseId}`, {}, {
            headers: {
                'Content-Type': 'application/json',
                'authorization': token
            }
        });
        console.log('HWID reset:', response.data);
    } catch (error) {
        console.error('Error resetting HWID:', error);
    }
};

resetHWID('license_id_here'); // Replace 'license_id_here' with your actual license ID
```

&nbsp;

