**Checklista för inloggning med egen IDP <ins>utan</ins> e-legitimation**

1.  Grundförutsättningen för att inloggningen mot provtjänsten ska
    fungera är att Skolhuvudmannen har tillgång till en egen
    inloggningstjänst (IDP) som är ansluten till federation som är
    medlem av interfederationen FIDUS.

2.  Provtjänstens Åtkomstgateway (med
    entityID=<https://skolverket.eduid.se/dnp/sp/>) måste finnas uppsatt
    som en service provider (SP) i inloggningstjänsten.
    *Notera: Vid tidigare tester med Fidustest användes Skolverkets åtkomstgateway trial med entityID=https://idpproxy.dev.eduid.se/sp.
    Denna byttes ut mot ovanstående åtkomstgateway prod (15 september 2023).*

4.  I samband med inloggning skall inloggningstjänsten ställa ut ett
    SAML-intyg som innehåller användarens eduPersonPrincipalName (EPPN)
    med;\
    \
    *FriendlyName=\"eduPersonPrincipalName\",\
    Name=\"urn:oid:1.3.6.1.4.1.5923.1.1.1.6\" samt
    NameFormat=\"urn:oasis:names:tc:SAML:2.0:attrname-format:uri\"*\
    \
    **OBS!**\
    För att det ska fungera så är viktigt att NameFormat används.
    Felaktigt uppsatt så kommer Provtjänstens Åtkomstgateway inte släppa
    igenom användarens EPPN till provtjänsten och användaren kommer inte
    lyckas med inloggningen. En nödlösning som visat sig fungera om inte NameFormat kan konfigureras i IDP är att skicka Name=\"eduPersonPrincipalName\" utan NameFormat.

5.  Det EPPN som används måste ha ett *scope* som överensstämmer med de
    *scope* som deklarerats i FIDUS metadata. *Scope* deklareras i
    IDP-metadatat som *Extensions* direkt efter elementet
    *IDPSSODescriptor*, se exempel;\
    \
    *\<IDPSSODescriptor
    protocolSupportEnumeration=\"urn:oasis:names:tc:SAML:2.0:protocol\"\>\
    \
    \<Extensions\>\
    \<shibmd:Scope xmlns:shibmd=\"urn:mace:shibboleth:metadata:1.0\"\
    regexp=\"false\"\>exempel.se\</shibmd:Scope\>\
    \</Extensions\>*\
    \
    **OBS!**\
    För att det ska fungera så är viktigt att *scope* i EPPN stämmer med
    det som deklarerats. Felaktigt uppsatt så kommer Provtjänstens
    Åtkomstgateway inte släppa igenom användarens EPPN till provtjänsten
    och användaren kommer inte lyckas med inloggningen.

6.  Genomför ett tekniskt verifieringstest för att se att det fungerar på Skolverkets testtjänst
    **[här](https://fidustest.skolverket.se/DNP/)**
