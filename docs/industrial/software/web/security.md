# JWT

# OAuth2

# SAML
		- https://gravitational.com/blog/how-saml-authentication-works/
		- https://en.wikipedia.org/wiki/SAML_2.0#SP_redirect_request;_IdP_POST_response
		- https://docs.oasis-open.org/security/saml/v2.0/saml-bindings-2.0-os.pdf
		- http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0-cd-02.html#5.1.2.SP-Initiated%20SSO:%20%20Redirect/POST%20Bindings|outline
		- http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0-cd-02.html#5.1.3.SP-Initiated%20SSO:%20%20POST/Artifact%20Bindings|outline
		- http://saml.xml.org/saml-specifications
		- http://saml.xml.org/wiki/sp-initiated-single-sign-on-postartifact-bindings
		- http://saml.xml.org/wiki/idp-initiated-single-sign-on-post-binding
		- http://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf (3.4.1 Element <AuthnRequest>) for schema details
		- https://blogs.oracle.com/dcarru/sp-vs-idp-initiated-sso
		- Azure: 
			- AuthnRequest: https://docs.microsoft.com/en-us/azure/active-directory/develop/single-sign-on-saml-protocol#authnrequest
			- Claims: https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-saml-claims-customization
			- SSO: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/what-is-single-sign-on#saml-sso
			- Setup: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications
			- Error AADSTS750054: https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/application-sign-in-problem-federated-sso-gallery#saml-request-not-present-in-the-request
			- Test SAML: https://docs.microsoft.com/en-us/azure/active-directory/azuread-dev/howto-v1-debug-saml-sso-issues
		- Okta:
			SAML: https://developer.okta.com/docs/concepts/saml/
		- OneLogin
			- https://www.samltool.com/generic_sso_req.php
			- https://developers.onelogin.com/saml/python
			- https://github.com/onelogin/python3-saml
			- AuthnRequest: https://developers.onelogin.com/saml/examples/authnrequest
			- SAMLRequest
				- https://github.com/onelogin/python3-saml/blob/a11c34103e0aa75ee1930471c492b5f8f69962c0/src/onelogin/saml2/auth.py#L378-L379
			- Setup
				- https://support.templafy.com/hc/en-us/articles/115005026225-How-to-setup-SSO-with-OneLogin-SAML-
			- Test
				- https://onelogin.service-now.com/support?id=kb_article&sys_id=83f71bc3db1e9f0024c780c74b961970
		- StackOverflow
			- https://stackoverflow.com/questions/30388926/http-redirect-binding-saml-request
		- Tools
			- deflate + b64emcode: https://www.samltool.com/encode.php
			- urlencode: https://www.urlencoder.org/