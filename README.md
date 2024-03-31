# AuthAPI-Docs

**Generating License Keys
To generate license keys, you would typically use the generateLicenses function defined in the /dashboard/src/services/apps.js file. This function sends a POST request to the backend to generate licenses for a specific app.**

```java
exports.generateLicenses = (async (component, id, duration, quantity) => {
    const response = await fetch(`${process.env.VUE_APP_ENDPOINT}/backend/dashboard/api/v1/apps/${id}/licenses`, {
        method: 'POST',
        body: JSON.stringify({
            duration: duration,
            quantity: quantity 
        }),
        headers: {
            'Content-Type': 'application/json',
            'authorization': component.$store.state.token
        }
    });
    
    const result = await response.json();

    if(result.status == "success")
    {
        return result.licenses;
    }
    else
    {
        component.$toast.error(result.message);
        return false;
    }
});
```
