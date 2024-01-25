## FAQ

Här samlar vi svar på vanliga förekommande frågor och lösningar på problem som andra användare stött i samband med uppsättning av inloggning mot Skolverkets provtjänst.

**1. Vi har konfigurerat vår IDP för inloggning mot Fidustest men användarens EPPN (eduPersonPrincipalName) stoppas i Provtjänstens åtkomstgateway och kommer inte fram till Fidustest.**

**Svar:**\
Två vanliga fel när EPPN stoppas i Provtjänstens åtkomstgateway är:\
    1. Scope inte deklarerat eller stämmer inte med Scope som deklarerats i IDP-metadata\
    2. EPPN skickas inte korrekt i det SAML-intyg som ställs ut av IDPn\
    \
    I det första fallet är det viktigt att scopet på användarens EPPN dvs det som kommer efter @ stämmer med det som deklarerats i IDP-metadatat. Endast EPPN med scope som finns deklarerade kommer släppas igenom Provtjänstens
    Åtkomstgateway.\
    \
    I det andra fallet så kontrollera att det SAML-intyg som ställs ut av IDPn har Name och NameFormat enligt nedan:\
    \
    *FriendlyName=\"eduPersonPrincipalName\",\
    Name=\"urn:oid:1.3.6.1.4.1.5923.1.1.1.6\" samt
    NameFormat=\"urn:oasis:names:tc:SAML:2.0:attrname-format:uri\"*\
    \
    För att det ska fungera korrekt så är viktigt att NameFormat används.\
    \
    (För Google och andra IDPer där NameFormat inte kan anges så ange endast Name=\"eduPersonPrincipalName\")\
    \
**2. Vi har en godkänd e-legitimation ansluten till vår IDP men när Skolpersonalen loggar in så blir det bara vanlig inloggning med användarnamn och lösenord, och dom kommer då inte in i Provtjänsten**\
\
**Svar:**\
Ett vanligt fel när inte flödet för egen IDP med ansluten e-legitimation fungerar är att stödet inte deklarerat korrekt i federationens metadata. Kontrollera att deklarationen överensstämmer med nedanstående:

*\<EntityDescriptor xmlns:ds=\"http://www.w3.org/2000/09/xmldsig#"
xmlns:saml=\"urn:oasis:names:tc:SAML:2.0:assertion"
xmlns:shibmd=\"urn:mace:shibboleth:metadata:1.0"
entityID=\"http://idp.exempel.se/">*
    
*\<Extensions\>\<mdattr:EntityAttributes
xmlns:mdattr=\"urn:oasis:names:tc:SAML:metadata:attribute">\<saml:Attribute
Name=\"urn:oasis:names:tc:SAML:attribute:assurance-certification\"
NameFormat=\"urn:oasis:names:tc:SAML:2.0:attrname-format:uri\"\>\<saml:AttributeValue\>https://fidus.skolverket.se/authentication/e-leg</saml:AttributeValue\>\</saml:Attribute\>\</mdattr:EntityAttributes\>\
\</Extensions\>*

**Obs!**\
Deklarationen måste finnas i \<Extensions\> direkt under \<EntityDescriptor\>. Finns deklarationen längre ner under \<IDPSSODescriptor\> så kommer den inte användas.\
\
**3. Vi har deklarerat WantAuthnRequestsSigned=“true” på IDPSSODescriptorn i vårt IDP-metadata men Provtjänstens åtkomstgateway signerar ändå inte autentiseringsbegäran.**\
\
**Svar:**\
Provtjänstens åtkomstgateway stödjer inte signering av autentiseringsbegäran. Det är inte heller något krav enligt SAML specifikationen eller federationen FIDUS. Vi rekommenderar därför att flaggan inte används i metadatat.

