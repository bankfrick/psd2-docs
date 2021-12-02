---
title: Bank Frick PSD2 Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell--sandbox: sandbox 
  - shell--production: production

toc_footers:
  - <a href='https://developers.bankfrick.li' target='_blank' rel='noopener noreferrer'>Visit Bank Frick Developers</a>
  - <a href='https://developers.bankfrick.li/signup' target='_blank' rel='noopener noreferrer'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/bankfrick/psd2-docs' target='_blank' rel='noopener noreferrer'>Edit on GitHub</a>

includes:
  - AIS
  - PIIS
  - MIS
  - PIS
  - SBS
  - Utility
  
search: true
---

# Bank Frick PSD2 API

## Available Enviroments (Environment URL)

  * Documentation: <a href="https://developers.bankfrick.li" target="_blank" rel="noopener noreferrer">Documentation</a>

## Bank Frick

  * Production: <a href="https://olb.bankfrick.li/" target="_blank" rel="noopener noreferrer">https://olb.bankfrick.li</a>
  * Sandbox: <a href="https://olbtest.bankfrick.li/" target="_blank" rel="noopener noreferrer">https://olbtest.bankfrick.li</a>
  * Contact E-Mail: <a href="mailto:help@bankfrick.li">help@bankfrick.li</a>

The api will be available under the following path:

BaseURL = <Environment URL>/xs2a/

Schemes: https

Please note that only the sandbox environment supports the example PSU-IDs, Passwords and IBANs mentioned under section Demo-Accounts.
A valid QWAC certificate is required for all environments except for the Documentation.

## Registration

As TPP you need to be registered for each bank separately. Please send us a short E-Mail with the following information:

  * An e-mail-adress to contact you
  * Name of your organisation
  * Webpage or your organisation
  * Roles in your certificate (for example "PSD_PI")
  * PSP-ID of your certificate (for example PSDDE-BAFIN-123456 - listed at OID 2.5.4.97)
  * trust services that signed your certificate

If you have any questions regarding executed API-calls, please send us a message containing the following additional informations:

  * X-Request-ID
  * URL (including any identifiers contained in the URL)
  * Date and Time of the request

## General Description

The Bank Frick PSD2 API - Package XS2A enables banks to comply with the requirements of the PSD2-to implement the directive.
It is based on the required account access APIs of the specifications of the EBA and the Berlin Group (NextGenPSD2).

For retrieving account information and initiating payments by third-party providers (TPPs) endpoints are provided:

Account Information Services (AIS)

  * Account list of all PSD2 relevant user accounts, optionally with account balance
  * Details of the specified account (identifier, type, name, currency, etc.), optionally with account balance
  * Account balance for specified user account
  * Transactions list for given user account
  * Detailed information on specified account activity (optional)
  * Consent for one-time account information access
  * Consent for recurring account information access (optional)
  * Detailed information on a given Consent
  * Status information for a given Consent
  * Consent deletion for recurring account information access (optional)

Payment Information Services (PIS)

  * Initiation of a payment
  * Detailed information on specified payment
  * Status information as to whether payment order has been accepted
  * Initiation of mass payments, scheduled payments, standing orders (incl. analog endpoints for detailed information, Status information) (if supported by the ASPSP)

Confirmation of Funds (PIIS)

  * Inquiry as to whether there is sufficient account coverage

Signing Baskets Service (SBS) (if supported by the ASPSP)

  * Streamline authorisation process by grouping transactions

Market Order Information Services (MIS) (if supported by the ASPSP)

  *  Details of specified custody accounts
  *  Search for financial instruments, optionally with rating information
  *  Initiation and update of a market order request
  *  Status information of a market order*

The APIs are

  * via pre-defined standard interfaces and integration tools into the environment of the Bank uniformly implemented in the form of REST JSON APIs
  * with the defined Consent oriented on the standards of the Berlin Group available in the "embedded" or "decoupled" characteristic

The Bank Frick Banking API provides all the relevant information and configurations of the PSD2-Application ready for the administrators of the bank.

## Some General Remarks Related to this version of the OpenAPI Specification

*  This API definition is based on the Implementation Guidelines of the Berlin Group PSD2 API. It is not an replacement in any sense. The main specification is (at the moment) always the Implementation Guidelines of the Berlin Group PSD2 API.
*  This API definition contains the REST-API for requests from the PISP to the ASPSP.
*  This API definition contains the messages for all different approaches defined in the Implementation Guidelines.
*  We omit the definition of all standard HTTP header elements (mandatory/optional/conditional) except they are mention in the Implementation Guidelines. Therefore the implementer might add these in his own realisation of a PSD2 complient API.

## General Remarks on Data Types

The character set is UTF 8 encoded. This specification is only using the basic data elements "String", "Boolean", "ISODateTime", "ISODate", "UUID" and "Integer" (with a byte length of 32 bits) and ISO based code lists. ASPSPs will accept for strings at least the following character set:

a b c d e f g h i j k l m n o p q r s t u v w x y z

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

0 1 2 3 4 5 6 7 8 9

* / - ? : ( ) . , ' +

`CrLf` Space

The characters `Cr` and `Lf` must never be used as single characters and must only be used together in the sequence `CrLf`, that is, `LfCr` is not allowed. When the character sequence `CrLf` is used in a field format with several lines, it is used to indicate the end of one line of text and the start of the next line of text.

<a href="https://www.berlin-group.org/" target="_blank" rel="noopener noreferrer">The Berlin Group - A European Standards Initiative - Website</a>

<a href="https://creativecommons.org/licenses/by/4.0/" target="_blank" rel="noopener noreferrer">Creative Commons Attribution 4.0 International Public License</a>

<a href="https://www.berlin-group.org/nextgenpsd2-downloads" target="_blank" rel="noopener noreferrer">Full Documentation of NextGenPSD2 Access to Account Interoperability Framework (General Introduction Paper, Operational Rules, Implementation Guidelines)</a>