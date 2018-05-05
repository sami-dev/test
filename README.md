<H1><font size="7" color="#e5474b">Managing Multiple Brand Experiences with a Single Okta Org</font></H1>

<div id="table-of-contents">
<h1><font color="e5474b">Table of Contents</font></h1>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">A. Introduction</a></li>
<li><a href="#sec-2">B. Prerequisites</a></li>
<li><a href="#sec-3">C. Build MVC Web Applications</a></li>
<li><a href="#sec-4">D. Setting up Okta's Preview Sandbox</a></li>
<li><a href="#sec-5">E. Configure, Deploy and Run Web Applications</a></li>
</ul>
</div>
</div>

# <font color="e5474b">A. Introduction</font><a id="sec-1" name="sec-1"></a>
**TODO**

# <font color="e5474b">B. Prerequisites</font><a id="sec-2" name="sec-2"></a>
Before you get started, you'll need to install or set up the
software and services below:

1.  Download and install [Visual Studio Community Edition](https://www.visualstudio.com/downloads/)     
    At this time, Visual Studio 2017 is the most recent version of Visual Studio available.

    <img src="Documentation/Images/vs-community.png" alt="Visual Studion Community"/>
	<br/>

2.  Sign up for [Okta Developer Edition](http://developer.okta.com/).    
    You'll need an Okta *organization* of your own to use as you follow this guide. After activating your account, log in to it. If you just created an account, you'll see a screen similar to the one below. Click on **< > Developer Console** in the top-left corner and switch to the Classic UI.
    
    <img src="Documentation/Images/okta-classic-ui.png" alt="Okta Dev Console" width="800"/> 
	<br/>

3.  *Optional:* Sign up for a [free trial of Microsoft Azure](http://azure.microsoft.com/en-us/pricing/free-trial/).
    
    This step is not required. You can run sample applications from your computer. However, if you want to host Branded Login pages and Web applications on a public-facing Website then Azure is the easiest place to do that. You can map custom Domain Names to Azure Web application. This will be useful for hosting multi-branded login page application.

	<br/>
	<img src="Documentation/Images/Azure-001.PNG" alt="Microsoft Azure Free" width="800"/> 
	<br/>


# <font color="e5474b">C. Build MVC Web Applications</font><a id="sec-3" name="sec-3"></a>
The Visual Studio solution that you have downloaded contains three projects.
Open solution file in Visual Studio. You should be able to see three projects and Build Solution.
	<br/>
	<img src="Documentation/Images/VS-001.png" alt="Visual Studio" /> 
	<br/>


1. **Okta.Clients.OpenIdConnect**: This is a sample **OpenID Connect** MVC Web application that demonstrate the use of branded login pages for a single Okta org.
	* It is a sample server-side Web application.
	* It uses Microsoft.Owin Middleware for OpenID Connect protocol implementation.
		<br/>
		<img src="Documentation/Images/VS-002.png" alt="Visual Studio" /> 
		<br/>
	* User is authenticated via selected branded login page 
	* Two brands are used in this sample: (a) Green Brand; and (b) Blue Brand  	
	* You can run this project locally (localhost) or publish this application on Microsoft Azure. 
		<br/>
		<img src="Documentation/Images/VS-002A.png" alt="Visual Studio" /> 
		<br/>
	* Set <b>Okta.Clients.OpenIdConnect</b> project as StartUp project and run application and you will see "Okta Multi-Branded Login Pages" page.
		<br/>
		<img src="Documentation/Images/VS-002B1.png" alt="Visual Studio" width="800" /> 
		<br/>
	* <b>Note</b>: To test the complete user authentication flow via Okta org see <a href="#sec-5">Section E</a>
		<br/>
2. **Okta.Clients.SAML2**: This is a sample **SAML 2.0** MVC Web application that demonstrate the use of branded login pages for a single Okta org.
	* It is a sample server-side Web application.
	* It uses Sustainsys.Saml2 NuGet package for SAML2 protocol implementation. 
		<br/>
		<img src="Documentation/Images/VS-003.png" alt="Visual Studio" /> 
		<br/>
	* User is authenticated via branded login pages. 
	* Two brands are used in this sample: (a) Green Brand; and (b) Blue Brand
	* You can run this project locally (localhost) or publish this application on Microsoft Azure.
		<br/>
		<img src="Documentation/Images/VS-003A.png" alt="Visual Studio" /> 
		<br/> 
	* Set **Okta.Clients.SAML2** project as StartUp project and run application and you will see "Okta Multi-Branded Login Pages" page.	
		<br/>
		<img src="Documentation/Images/VS-003B.png" alt="Visual Studio" width="800" /> 
		<br/>
	*  <b>Note</b>: To test the complete user authentication flow via Okta org see <a href="#sec-5">Section E</a>
		<br/>
3. **OktaLogin**: This is a MVC Web application that uses Okta Sign-in widget for user authentication.
	* It is server-side MVC Web application
	* It uses <b>Okta Sign-In Widget</b> for user authentication. The Okta Sign-In Widget is a JavaScript library that gives you a fully-featured and customizable login experience which can be used to authenticate users on any website <a href="https://developer.okta.com/code/javascript/okta_sign-in_widget" target="_blank">Okta Sign-IN Widget Guide</a>	
	* Two brands are used in this sample: (a) Green Brand; and (b) Blue Brand
	* For each brand, there is a separate style sheet: (a) Style-Blue.css; and (b) Style-Green.css 
	* It also supports multiple languages (System.Globalization)
	* You can run this project locally (localhost) or publish this application on Microsoft Azure. There are several advantages on hosting on Azure including identifying brand based on hostname.    
		<br/>
		<img src="Documentation/Images/VS-004A.png" alt="Visual Studio" /> 
		<br/> 
	* Set **OktaLogin** project as StartUp project and run application with below parameters and you will see "Blue Brand Login Page" page. <a href="#">http://localhost:12411/?brand=blue&RelayState=2121</a>	
		<br/>
		<img src="Documentation/Images/VS-004C.png" alt="Visual Studio" width="800" /> 
		<br/>
	* To see "Green Brand Login Page", run with these parameters. <a href="#">http://localhost:12411/?brand=green&RelayState=2121</a>
		<br/>
		<img src="Documentation/Images/VS-004D.png" alt="Visual Studio" width="800" /> 
		<br/>
	* <b>Note</b>: To test the complete user authentication flow via Okta org see <a href="#sec-5">Section E</a>
		<br/>
# <font color="e5474b">D. Setting up Okta's Preview Sandbox</font><a id="sec-4" name="sec-4"></a>

1. Create a Custom Authorization Server
2. Create Identity Providers for Each Branded Login Page
3. Enabling CORS (Trusted Origins)
4. Create Test User Accounts for Each Brand (Add Person)
5. Create Groups
6. Add OpenID Connect and SAML 2.0 Applications

## <font color="#6666ff">Step 1. Create a Custom Authorization Server</font> ##

Okta allows you to create custom OAuth 2.0 authorization servers. Create a new custom authorization server for this application.

1. Go to <font color="#e5474b">**Security → API → Authorization Servers**</font>
2. Click on <font color="#e5474b">**"Add authorization server"**</font> button

	<img src="Documentation/Images/AuthServer-001.png" alt="Add Authorization Server" />

3.  Provide below information and click on Save button.

	* Name: Franchisor Org Auth
	* Audience: https://franchisor.org.com
	* Description: Authorization server for franchisor 

4.  It will add a custom authorization server.

	<img src="Documentation/Images/AuthServer-002.png" alt="Add Authorization Server" />

5.  Access Policies:

	By default, there is no access policies. We will add access policies for our sample application later.

## <font color="#6666ff">Step 2. Create Identity Providers for Each Branded Login Page</font> ##
Okta allows you to create Identity Providers to manage federations with external Identity Providers (IdP). Each identity provider (IdP) requires some setup. For this application, we will create an Identity Provider for each branded login page.

1. Go to <font color="#e5474b">**Security → API → Identity Providers**</font>
	<img src="Documentation/Images/IdP-001.png" alt="Add Identity Provider"/>

### 2.1	Create Identity Provider for "Green Brand Login Page" ###
This is for Green Brand. This will not be acted as true identity provider. This will not do traditional SAML 2.0 Request/Response (as SAML2 functionaliy is never used). Its only job to host login page, which contains the sign-in widget. 
 
1. Click on <font color="#e5474b">**"Add Identity Provider"**</font> button
2. Select “Add SAML 2.0 IdP”
	<br/>
	<img src="Documentation/Images/IdP-002A.png" alt="Add Identity Provider"/>
	<br/><br/>
3. Provide fields for new Identity Provider
	* Name: Green Brand Login Page
	* IdP Username: idpuser.subjectNameId
	* Filter: Unchecked
	* Match against: Okta Username
	* If No match is found: Redirect to Okta Sign-in Page
	* SAML Protocol Settings:
	* IdP Issuer URI: Provide URL for Green branded Login Page. 
		For Example: https://demo.login.greenbrand.com
	* IdP Single Sign-on URI: Provide URL for Green brand Login Page URL.
		This is the URL where login page application is hosted. Unauthenticated user will be redirected there. 
		For Example: https://demo.login.greenbrand.com
	* Request Binding: HTTP POST
	* Request Signature: Unchecked
	* Rest of the fields : Default Values
	<img src="Documentation/Images/IdP-003.png" alt="Add Identity Provider"/>
	<br/>
	<img src="Documentation/Images/IdP-004.png" alt="Add Identity Provider"/>
	<br/>
4.  It will create a new SAML 2.0 Identity Provider
	<br/>
	<img src="Documentation/Images/IdP-005A.png" alt="Add Identity Provider"/>
	<br/>
	* Note: The last part of Assertion Consumer Service (ACS) URL provides **idp** value. This value be will be sent as **idp** query string parameter value to pick green branded login page.

### 2.2	Create Identity Provider for "Blue Brand Login Page" ###
This is for Blue Brand. This will not be acted as true identity provider. This will not do traditional SAML 2.0 Request/Response (as SAML2 functionaliy is never used). Its only job to host login page, which contains the sign-in widget. 

1. Click on <font color="#e5474b">**"Add Identity Provider"**</font> button
2. Select “Add SAML 2.0 IdP”
	<img src="Documentation/Images/IdP-002A.png" alt="Add Identity Provider"/>
3. Provide fields for new Identity Provider
	* Name: Blue Brand Login Page
	* IdP Username: idpuser.subjectNameId
	* Filter: Unchecked
	* Match against: Okta Username
	* If No match is found: Redirect to Okta Sign-in Page
	* SAML Protocol Settings:
	* IdP Issuer URI: Provide URL for Blue branded Login Page.
		For Example: https://demo.login.bluebrand.com
	* IdP Single Sign-on URI: Provide URL for Blue brand Login Page URL. 
		This is the URL where login page application is hosted. Unauthenticated user will be redirected there. 
		For Example: https://demo.login.bluebrand.com
	* Request Binding: HTTP POST
	* Request Signature: Unchecked
	* Rest of the fields : Default Values
	<br/><br/>
	<img src="Documentation/Images/IdP-006.png" alt="Add Identity Provider"/>
	<br/>
	<img src="Documentation/Images/IdP-007.png" alt="Add Identity Provider"/>
	<br/>
4. It will create a new SAML 2.0 Identity Provider
	<br/>
	<img src="Documentation/Images/IdP-008.png" alt="Add Identity Provider"/>
	<br/>
	* Note: The last highlighted part of Assertion Consumer Service (ACS) URL provides **idp** value. This value be will be sent as **idp** query string parameter value to pick green branded login page.

## <font color="#6666ff">Step 3. Enabling CORS (Trusted Origins)</font> ##
In Okta, CORS (Cross-Origin Resource Sharing) allows JavaScript hosted on your websites to make an XHR to the Okta API with the Okta session cookie. Every website origin must be explicitly permitted via the administrator UI for CORS. You have to enable CORS for the Branded Login pages.

**Go to <font color="#e5474b">Security → API → Trusted Origins**</font>

### 3.1 Add CORS for Green Brand Login Page ###
- Click on <font color="#e5474b">**Add Origin**</font>
	* Name: Green Brand Login
	* Origin URL: Provide Branded Login Page URL e.g. https://demo.login.greenbrand.com
	* Type: CORS [Checked] Redirect [Unchecked]
- Click on <font color="#e5474b">**Save**</font> button
	<br/>
	<img src="Documentation/Images/Cors-001.png" alt="Add CORS"/>
	<br/>
### 3.2 Add CORS for Blue Brand Login Page ###
- Click on <font color="#e5474b">**Add Origin**</font>
	* Name: Blue Brand Login
	* Origin URL: Provide Branded Login Page URL e.g. https://demo.login.bluebrand.com
	* Type: CORS [Checked] Redirect [Unchecked]
- Click on <font color="#e5474b">**Save**</font> button
	<br/>
	<img src="Documentation/Images/Cors-002.png" alt="Add CORS"/>
	<br/>
	Now, you should have **two CORS** in the list of Origins
	<br/>
	<img src="Documentation/Images/Cors-003.png" alt="Add CORS"/>
	<br/>

## <font color="#6666ff">Step 4. Create Test User Accounts for Each Brand (Add Person)</font> ##
Now, we will add two test accounts in Okta. Use the People page to add test users.

Go to <font color="#e5474b">**Directory → People**</font>

### 4.1 Add Test User Account for Green Brand ###
Enter a test user account for Green Brand. For Example: John.Doe@greenbrand.com

- Click on <font color="#e5474b">**Add Person**</font>
	* First Name: John
	* Last Name: Doe
	* Username: John.Doe@greenbrand.com
	* Primary Email: John.Doe@greenbrand.com
	* Password: set by admin
	* Password: provide value
	* [Unchecked] User must change password on first login 
	<br/>
	<img src="Documentation/Images/Person-001.png" alt="Add Person"/>
	<br/>

### 4.2 Add Test User Account for Blue Brand ###
Enter a test user account for Green Brand. For Example: Jane.Doe@bluebrand.com

- Click on <font color="#e5474b">**Add Person**</font>
	* First Name: Jane
	* Last Name: Doe
	* Username: Jane.Doe@bluebrand.com
	* Primary Email: Jane.Doe@bluebrand.com
	* Password: set by admin
	* Password: provide value
	* [Unchecked] User must change password on first login 
	<br/>
	<img src="Documentation/Images/Person-002.png" alt="Add Person"/>
	<br/>
	Go to Directory -> People. Now, you should see both test accounts.
	<br/>
	<img src="Documentation/Images/Person-003.png" alt="Add Person"/>
	<br/>

## <font color="#6666ff">Step 5. Create Groups</font> ##
Its easier to manage users and applications by creating groups. Now, we will create two brand groups and add test accounts to those groups. 

Go to <font color="#e5474b">**Directory → Groups**</font> 

### 5.1 Add GreenBrand Group ###
Create a group for Green Brand users.

- Click on <font color="#e5474b">**Add Group**</font>
	* Name: GreenBrand Group
	* Description: Users belong to Green Brand
	<br/>
	<img src="Documentation/Images/Groups-001.png" alt="Add Person"/>
	<br/>
- Assign John.Doe@GreenBrand.com to GreenBrand Group
	<br/>
	<img src="Documentation/Images/Groups-002.png" alt="Add Person"/>
	<br/>
 

### 5.2 Add BlueBrand Group ###
Create a group for Blue Brand users.

- Click on <font color="#e5474b">**Add Group**</font>
	* Name: BlueBrand Group
	* Description: Users belong to Blue Brand
	<br/>
	<img src="Documentation/Images/Groups-003.png" alt="Add Person"/>
	<br/>
- Assign Jane.Doe@BlueBrand.com to BlueBrand Group
	<br/>
	<img src="Documentation/Images/Groups-004.png" alt="Add Person"/>
	<br/>
- Go to Directory -> Groups, you should be able to see both groups (with one user member)
	<br/>
	<img src="Documentation/Images/Groups-005.png" alt="Add Person"/>
	<br/>

## <font color="#6666ff">Step 6. Add OpenID Connect and SAML 2.0 Applications</font> ##
Okta allows you to configure OpenID Connect or SAML2 Web applications. 

Go to <font color="#e5474b">**Applications → Applications**</font>


### 6.1 Add OpenID Connect Branded Application ###
Lets first add OpenID connect branded Web Application.

- Click on <font color="#e5474b">**Add Application**</font> button
	<br/>
	<img src="Documentation/Images/App-001.png" alt="Add Application"/>
	<br/>	
- Click on <font color="#e5474b">**Create New App**</font> button
	<br/>
	<img src="Documentation/Images/App-002.png" alt="Add Application"/>
	<br/>
- New Application Integration
	
	* Platform: Web
	* Sign on Method: OpenID Connect
	<br/>
	<img src="Documentation/Images/App-003A.png" alt="Add Application"/>
	<br/>
- Provide OpenID Connect Application Integration details

	* Application Name: OpenID Connect WebApp
	* Application Logo: [optional]
	* Login Redirect URIs: provide Login URL for application 
		e.g. https://oktane2018openidconnect.azurewebsites.net/
	* Logout Redirect URIs: provide Logout URL for application
		e.g. https://oktane2018openidconnect.azurewebsites.net/
		<br/>
		<img src="Documentation/Images/App-004.png" alt="Add Application"/>
		<br/>
- Edit Application Configuration:

	* Select Grant Types: 
		* Authorization Code
		* Implicit (Hybrid) - Allow ID Token
	* Click on <font color="#e5474b">**Save**</font> button to save changes.
	* Note: Client Credentials are needed for application configuration
	<br/>
	<img src="Documentation/Images/App-005A.png" alt="Add Application"/>
	<img src="Documentation/Images/App-005B.png" alt="Add Application"/>
	<img src="Documentation/Images/App-006.png" alt="Add Application"/>
	<br/>
- Assign application to groups:

	* BlueBrand Group
	* GreenBrand Group
	<br/>
	<img src="Documentation/Images/App-007.png" alt="Add Application"/>
	<br/>
- Go to Applications List. You will see newly added application.
	<br/>
	<img src="Documentation/Images/App-008.png" alt="Add Application"/>
	<br/>
- Add Access Policy for application:
	* Go to Authorization Server.
	* Go to <font color="#e5474b">**Security → API**</font>
	* Select Authorization server
	<br/>
	<img src="Documentation/Images/App-009.png" alt="Add Application"/>
	<br/>
- Go to Access Policies under Authorization Server
	* Add New Access Policy (if not already exists)
	* Click on <font color="#e5474b">**Add Policy**</font> button.
	<br/>
	<img src="Documentation/Images/App-010.png" alt="Add Application"/>
	<br/>
- Provide information for Access Policy

	* Name: OpenID Connect WebApp Policy
	* Description: Access Policy for OpenID Connect WebApp
	* Select the <font color="#e5474b">**OpenID Connect Web App**</font>
	* Click on <font color="#e5474b">**Create Policy**</font> button
	<br/>
	<img src="Documentation/Images/App-011.png" alt="Add Application"/>
	<br/>
- Add User Access Rule for OpenID Connect Web Application
	* Rule Name: User Access Rule
	<br/>
	<img src="Documentation/Images/App-012.png" alt="Add Application"/>
	<br/>
- Review Access Policy for the OpenID Connect Web Application
	<br/>
	<img src="Documentation/Images/App-013.png" alt="Add Application"/>
	<br/>
### 6.2 Add OpenID Connect Client Proxy Application for SAML2 Applications ###
Now, we will configure an OpenID Connect Client Proxy Application. This will be used as proxy for redirecting user to branded login page (for all SAML applications).

- Click on <font color="#e5474b">**Add Application**</font> button
	<br/>
	<img src="Documentation/Images/App-001.png" alt="Add Application"/>
	<br/>	
- Click on <font color="#e5474b">**Create New App**</font> button
	<br/>
	<img src="Documentation/Images/App-002.png" alt="Add Application"/>
	<br/>
- New Application Integration
	
	* Platform: Web
	* Sign on Method: OpenID Connect
	<br/>
	<img src="Documentation/Images/App-003A.png" alt="Add Application"/>
	<br/>
 
- Provide Application Name and Logo

	* Application Name: SAML2 Custom Login Page OIDC Client
	* Application Logo: Optional

	* Provide Login Redirect URIs: For every SAML 2 app that want to use branded login page,  we must configure redirect URL for that SAML app that will reissue SAML2 AuthN request. In response, Okta will send SAML response.
		* For Example: Green Brand Application SingIn Link
		https://oktane2018saml2.azurewebsites.net/SignIn/Link?Brand=GREEN
		* For Example: Blue Brand Application SingIn Link
		https://oktane2018saml2.azurewebsites.net/SignIn/Link?Brand=BLUE
	<br/>
	<img src="Documentation/Images/App-014.png" alt="Add Application"/>
	<br/>
	* Allowed Grant Type: [checked]Authorization Code
	<br/>
	<img src="Documentation/Images/App-015A.png" alt="Add Application"/>
	<br/>
	<br/>
	<img src="Documentation/Images/App-016A.png" alt="Add Application"/>
	<br/>
	* This **client ID** in client credentials section will be used in every SAML2 application configuration. 
	* Assign this application to Everyone group. Because this application will be a common Proxy application for all SAML applications
	<br/>
	<img src="Documentation/Images/App-017.png" alt="Add Application"/>
	<br/> 

### 6.3 Configure SAML 2.0 Green Brand Application ###
For SAML branded application, we will have to create separate configuration for each brand. Now, we will add SAML 2.0 Green Brand application.

- Click on <font color="#e5474b">**Add Application** </font>button
	<br/>
	<img src="Documentation/Images/App-001.png" alt="Add Application"/>
	<br/>	
- Click on <font color="#e5474b">**Create New App**</font> button
	<br/>
	<img src="Documentation/Images/App-002.png" alt="Add Application"/>
	<br/>
- New Application Integration
	
	* Platform: Web
	* Sign on Method: SAML 2.0
	<br/>
	<img src="Documentation/Images/App-018A.png" alt="Add Application"/>
	<br/> 
- SAML Integration
	* Provide App Name: SAML2 Green WebApp
	<br/>
	<img src="Documentation/Images/App-019.png" alt="Add Application"/>
	<br/>

- SAML Settings:
	* Single Sign On URL: Provide Sign On URL e.g. https://oktane2018saml2.azurewebsites.net/Saml2/Acs
	* Recipient URL: Same as Sign On URL
	* Destination URL: Same as Sign On URL
	* Audience Restriction: e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Name ID Format: Unspecified
	* Response: Signed
	* Assertion Signature: Signed
	<br/>
	<img src="Documentation/Images/App-020.png" alt="Add Application"/>
	<br/>
- SAML Logout Setting: click on Show Advance Settings and Provide Single Logout URL and Certificate
	* SAML Single Logout: Enabled 
	* Signle Logout URL: e.g. https://oktane2018saml2.azurewebsites.net/
	* SP Issuer: Provide issuer e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Signature Certificate: Upload certificate file
	<br/>
	<img src="Documentation/Images/App-021.png" alt="Add Application"/>
	<br/>
- SAML Attributes: Provide attributes that will be available in SAML response
	* uid
		* Name: uid
		* Name format: Unspecified
		* Value: user.id
	* orgid
		* Name: orgid
		* Name format: Basic
		* Value: value of OrgId e.g. 00oen1q08omzCcwsC0h7
	* brand
		* Name: brand
		* Name format: Basic
		* Value: GREEN
	* name
		* Name: name
		* Name format: Unspecified
		* Value: user.displayName
	* firstName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
		* Name format: Unspecified
		* Value: user.firstName
	* lastName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
		* Name format: Unspecified
		* Value: user.lastName
	* login
		* Name: login
		* Name format: Unspecified
		* Value: user.login
	* email
	 	* Name: email
	 	* Name format: Unspecified
	 	* Value: user.email
	<br/>
	<img src="Documentation/Images/App-022.png" alt="Add Application"/>
	<br/>
- Feedback:
	<br/>
	<img src="Documentation/Images/App-023.png" alt="Add Application"/>
	<br/>
- Configure Login Page URL: Provide Login Page URL for Green Brand SAML Application. This link will include: 

	* **client_id**: It is the Client ID for Proxy OpenID Connect App. 
	* **redirect_uri** : It is the endpoint for SAML2 application that will issue Sign-in request.This URL must be defined as valid URL in Proxy app. 
	* **idp**: It is the value for green branded login page (IdP).
    * **Authorize Endpoint**: First part is authorize end point of custom authorization server e.g. https://dev-217355.oktapreview.com/oauth2/auseqf1tfe6bvmQpP0h7/v1/authorize

    <br/>
	<img src="Documentation/Images/App-024A.png" alt="Add Application"/>
	<br/>
- Assign group to application: Assign GreenBrand Group
	<br/>
	<img src="Documentation/Images/App-025.png" alt="Add Application"/>
	<br/>
### 6.4 Configure SAML 2.0 Blue Brand Application ###
For SAML branded application, we will have to create separate configuration for each brand. Now, we will add SAML 2.0 Blue Brand application.

- Click on <font color="#e5474b">**Add Application**</font> button
	<br/>
	<img src="Documentation/Images/App-001.png" alt="Add Application"/>
	<br/>	
- Click on <font color="#e5474b">**Create New App**</font> button
	<br/>
	<img src="Documentation/Images/App-002.png" alt="Add Application"/>
	<br/>
- New Application Integration:
	
	* Platform: Web
	* Sign on Method: SAML 2.0
	<br/>
	<img src="Documentation/Images/App-018A.png" alt="Add Application"/>
	<br/> 
- SAML Integration:
	* Provide App Name: SAML2 Blue WebApp
	<br/>
	<img src="Documentation/Images/App-026.png" alt="Add Application"/>
	<br/>

- SAML Settings:
	* Single Sign On URL: Provide Sign On URL e.g. https://oktane2018saml2.azurewebsites.net/Saml2/Acs
	* Recipient URL: Same as Sign On URL
	* Destination URL: Same as Sign On URL
	* Audience Restriction: e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Name ID Format: Unspecified
	* Response: Signed
	* Assertion Signature: Signed
	<br/>
	<img src="Documentation/Images/App-020.png" alt="Add Application"/>
	<br/>
- SAML Logout Setting: click on Show Advance Settings and Provide Single Logout URL and Certificate
	* SAML Single Logout: Enabled 
	* Signle Logout URL: e.g. https://oktane2018saml2.azurewebsites.net/
	* SP Issuer: Provide issuer e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Signature Certificate: Upload certificate file
	<br/>
	<img src="Documentation/Images/App-021.png" alt="Add Application"/>
	<br/>
- SAML Attributes: Provide attributes that will be available in SAML response
	* uid
		* Name: uid
		* Name format: Unspecified
		* Value: user.id
	* orgid
		* Name: orgid
		* Name format: Basic
		* Value: value of OrgId e.g. 00oen1q08omzCcwsC0h7
	* brand
		* Name: brand
		* Name format: Basic
		* Value: BLUE
	* name
		* Name: name
		* Name format: Unspecified
		* Value: user.displayName
	* firstName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
		* Name format: Unspecified
		* Value: user.firstName
	* lastName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
		* Name format: Unspecified
		* Value: user.lastName
	* login
		* Name: login
		* Name format: Unspecified
		* Value: user.login
	* email
	 	* Name: email
	 	* Name format: Unspecified
	 	* Value: user.email
	<br/>
	<img src="Documentation/Images/App-027.png" alt="Add Application"/>
	<br/>
- Feedback:
	<br/>
	<img src="Documentation/Images/App-023.png" alt="Add Application"/>
	<br/>
- Configure Login Page URL: Provide Login Page URL for Blue Brand SAML Application. This link will include:
	* **client_id**: It is the Client ID for Proxy OpenID Connect App. 
	* **redirect_uri** : It is the endpoint for SAML2 application that will issue Sign-in request.This URL must be defined as valid URL in Proxy app. 
	* **idp**: It is the value for green branded login page (IdP).
    * **Authorize Endpoint**: First part is authorize end point of custom authorization server e.g. https://dev-217355.oktapreview.com/oauth2/auseqf1tfe6bvmQpP0h7/v1/authorize
	<br/>
	<br/>
	<img src="Documentation/Images/App-028A.png" alt="Add Application"/>
	<br/>
	<br/>
- Assign group to application: Assign BlueBrand Group
	<br/>
	<img src="Documentation/Images/App-029.png" alt="Add Application"/>
	<br/>

### 6.5 Configure SAML 2.0 Okta Application ###
For SAML branded application, we will have to create separate configuration for each brand. Now, we will add SAML 2.0 Okta application that will show default Okta login page.
This application will not use any of the custom login pages. 

- Click on <font color="#e5474b">**Add Application**</font> button
	<br/>
	<img src="Documentation/Images/App-001.png" alt="Add Application"/>
	<br/>	
- Click on <font color="#e5474b">**Create New App**</font> button
	<br/>
	<img src="Documentation/Images/App-002.png" alt="Add Application"/>
	<br/>
- New Application Integration:
	
	* Platform: Web
	* Sign on Method: SAML 2.0
	<br/>
	<img src="Documentation/Images/App-018.png" alt="Add Application"/>
	<br/> 
- SAML Integration:
	* Provide App Name: SAML2 Blue WebApp
	<br/>
	<img src="Documentation/Images/App-030.png" alt="Add Application"/>
	<br/>

- SAML Settings:
	* Single Sign On URL: Provide Sign On URL e.g. https://oktane2018saml2.azurewebsites.net/Saml2/Acs
	* Recipient URL: Same as Sign On URL
	* Destination URL: Same as Sign On URL
	* Audience Restriction: e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Name ID Format: Unspecified
	* Response: Signed
	* Assertion Signature: Signed
	<br/>
	<img src="Documentation/Images/App-020.png" alt="Add Application"/>
	<br/>
- SAML Logout Settings: click on Show Advance Settings and Provide Single Logout URL and Certificate
	* SAML Single Logout: Enabled 
	* Signle Logout URL: e.g. https://oktane2018saml2.azurewebsites.net/
	* SP Issuer: Provide issuer e.g. https://www.oktane2018.com/okta.clients.SAML2
	* Signature Certificate: Upload certificate file
	<br/>
	<img src="Documentation/Images/App-021.png" alt="Add Application"/>
	<br/>
- SAML Attributes: Provide attributes that will be available in SAML response
	* uid
		* Name: uid
		* Name format: Unspecified
		* Value: user.id
	* orgid
		* Name: orgid
		* Name format: Basic
		* Value: value of Okta OrgId e.g. 00oen1q08omzCcw####
	* brand
		* Name: brand
		* Name format: Basic
		* Value: OKTA
	* name
		* Name: name
		* Name format: Unspecified
		* Value: user.displayName
	* firstName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
		* Name format: Unspecified
		* Value: user.firstName
	* lastName
		* Name: http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
		* Name format: Unspecified
		* Value: user.lastName
	* login
		* Name: login
		* Name format: Unspecified
		* Value: user.login
	* email
	 	* Name: email
	 	* Name format: Unspecified
	 	* Value: user.email
	<br/>
	<img src="Documentation/Images/App-031.png" alt="Add Application"/>
	<br/>
- Feedback:
	<br/>
	<img src="Documentation/Images/App-023.png" alt="Add Application"/>
	<br/>
- Configure Login Page URL: Use the default organization login page
	<br/>
	<img src="Documentation/Images/App-032.png" alt="Add Application"/>
	<br/>
- Assign group to application: Assign both GreenBrand Group and BlueBrand Group
	<br/>
	<img src="Documentation/Images/App-033.png" alt="Add Application"/>
	<br/>


# <font color="e5474b">E. Configure, Deploy and Run Web Applications</font><a id="sec-5" name="sec-5"></a>
TODO - Run and Test Web Applications
App Settings - Web.Config for each project
OIDC - Notification handler for Startup file 
Normally, OIDC will determine brand from hostname. For this demo, we will use Id 
SAML2: Startup - SecurityIdentityProvider

Login Pages: Map Relay State to redirect URL
SignIn Controller - Send relaystate back to Authorization server
MVC App - stylesheets for each brand - responsive design - internationalized - Okta Sign-in widget support internationalization 

Sections - for WebConfig
2 Apps - Unprotected, Login page and User profile page (for each)
Azure - deployment