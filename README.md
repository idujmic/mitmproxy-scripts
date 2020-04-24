# controlled-update-of-software-components

This repository contains mitmproxy scripts to monitor parallel usage of two instances of a same application. One application can be patched and the other not so that we have two versions od the same application. The main idea is to connect to one version and interact with the application in a web browser. Proxy intercepts the traffic and apply it to the other version. While the proxy manipulates with the traffic, it also forwards the responses to another component that compares them. The compare component can search for differences in the responses for the same path. This way we can indicate potential bugs and vulnerabilites in the code. If one version of the application is updated and the other is original, we can indicate some unwanted differences that were created by the updates. That way we can control updates of software components

> Web application used for testing are:
>- eShopOnWeb: https://github.com/dotnet-architecture/eShopOnWeb
>- ColourAPI: https://github.com/binarythistle/ColourAPI 

The main scripts are new_script.py and new_compare.py.  
new_script.py is a mitmproxy script used for traffic manipulation. When we interact with one version of the application in the browser, the only way for that traffic to the other version is to reddirect the copied traffic. Copying the traffic is not enough because applications have random generated tokens, cookies and similar page components. User needs to specify which tokens are generated by the application in order to use the script. Once when the tokens are specified the script can adjust the traffic for the other version of the application.  
new_compare.py compares responses from instances of the application. Some differences can be legal, for example tokens that are generated. Legal differences are specified by the user. When comparing the responses, script uses the diff tool to get the differences. Then it goes through the response and checks if the differences are legal. 

## Tools
> Docker  
> mitmproxy
