## FAQ

Här samlar vi svar på vanliga förekommande frågor och lösningar på problem som andra användare stött i samband med uppsättning av inloggning mot Skolverkets provtjänst.

1. Vi har konfigurerat vår IDP för inloggning mot Fidustest men användarens EPPN (eduPersonPrincipalName) stoppas i Provtjänstens åtkomstgateway och kommer inte fram till Fidustest.\
\
**Svar:**\
Två vanliga fel när EPPN stoppas i Provtjänstens åtkomstgateway är:
    1. Scope inte deklarerat eller stämmer inte med Scope som deklarerats i IDP-metadata
    2. EPPN skickas inte korrekt i det SAML-intyg som ställs ut av IDPn

    I det första fallet är det viktigt att scopet på användarens EPPN dvs det som kommer efter @ stämmer med det som deklarerats i IDP-metadatat. Endast EPPN med scope som finns deklarerade kommer släppas igenom Provtjänstens
    Åtkomstgateway.

    I det andra fallet så kontrollera att det SAML-intyg som ställs ut av IDPn ser ut enligt nedan:\
    *FriendlyName=\"eduPersonPrincipalName\",\
    Name=\"urn:oid:1.3.6.1.4.1.5923.1.1.1.6\" samt
    NameFormat=\"urn:oasis:names:tc:SAML:2.0:attrname-format:uri\"*\
    \
    För att det ska fungera korrekt så är viktigt att NameFormat används.
    (En nödlösning som visat sig fungera om inte NameFormat kan konfigureras i IDP är att skicka Name=\"eduPersonPrincipalName\" utan NameFormat.)
