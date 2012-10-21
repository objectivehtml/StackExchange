# ExpressionEngine StackExchange API Spec

### Version

0.1.0 (2012-10-21)

### Contributors

- Objective HTML

### Overview

StackExchange provides an excellent Q&A format that has been proven to be very effective. However, almost all developers would agree that it would be far too time consuming and produce inferior results if every site rolled their own variation. The purpose of this document is to get community collaboration on how to provide the best support possible by integrating the StackExchange API into our websites all in an effort to provide high quality and standardized public support. This document is written for developers but it is encouraged that all users give feedback, so we (the developers) can provide the best support we can in the least amount of time.

---

### Standard API Calls

First and foremost, port all the API methods into standard EE tags. Using a single *api* endpoint, and use a fourth segment to denote the API method to be called.

	{exp:stackexchange:api:method_name arg1="value1" arg2="value2" arg3="value3"}
	
		{variable_name}
		
		{some_tagpair param1="value1" param2="value2"}
			
			{some_variable_1}
			{some_variable_2}
			{some_variable_3}
			
		{/some_tagpair}
		
	{/exp:stackexchange:api:method_name}

### Advanced API calls

Standard EE tags will perform more advanced calls, often performing multiple requests to the API. These methods will make advanced integration much easier.

	{exp:stackexchange:method_name param1="value1" param2="value2"}
		
		[...]
		
	{/exp:stackexchange:method_name}

---

### Searchable Knowledgebase

The main objective of these methods would be to allow users to easily search for other questions/answers, and easily fetch all the associated meta data. This data would be parsed into various EE variables and tag pairs.

1. Method to create a standalone search/results page that allows users to search StackExchange for questions and answers.
2. Method to peform the same type of searches listed above, except without the need for submitting a form.
3. Questions/Answer detail pages that will reference the post by a specific ID
4. Get related information based on a spefic question ID
5. EE tags should provide variables and tag pairs to get comments and other associated meta data

### Dynamic Links

1. Provide EE tags to create dynamic links that will assist users in creating posts that have already been tagged appropriately. http://meta.stackoverflow.com/questions/33195/can-i-have-a-link-to-the-ask-as-question-page-with-the-tag-field-pre-filled/67699#67699
2. SAEF that would do the same as above except users fill in a form and that data is then sent to the StackExchange.

### Caching

Caching should be built into the core. Using config files, one could adjust the cache length. This would minimize all requests to the server.

### Abstraction

Abstraction is the utmost importance here. All code should 100% DRY with a clear architecture in mind. Here is a basic outline of the core proposed architecture.

- Base Class
	- setters
	- getters
	- common properties

- Core Class/extends Base Class
	- http/curl
	- loader method

- Cache Driver/extends Base Class
	- basic CRUD
	- load config files to get cache length
	
- API Driver/extends Base Class
	- sends requests to the API endpoints


*Subclasses would be considered 'drivers'. Drivers could perform any additional custom logic not a part of the core API. This will allow for a scalable architecture so if StackExchange adds new features, the core API won't have to be changes. Additionally, if other developers want to integrate even more custom features, drivers will be a way for people to use the core API without hacking or breaking existing code. Drivers and extendible architecture is critical to success and for developer adoption.*

---

### How to Contribute?

All the proposed code is intended to be open source. It's intended for everyone to benefit from this migration to StackExchange. There is clearly a lot of momentum to be involved, and getting developers on board will only make things easier. Non developers can contributes with ideas, features, and commenting on how you would like to see improved support. 

If anyone knows a lot about licensing, this project will need one. This is intended to be a community effort, and it's encouraging to see the all the support for the movement.