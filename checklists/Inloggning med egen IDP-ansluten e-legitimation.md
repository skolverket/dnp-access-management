**Checklista: Inloggning <ins>med</ins> egen IDP-ansluten
e-legitimation**

1.  Grundförutsättningar för att inloggning med egen IDP-ansluten
    e-legitimation ska fungera är;

    a.  Inloggning <ins>utan</ins> e-legitimation inloggning fungerar
        enligt checklista och tekniskt verifieringstest

    b.  Att IDP har en DIGG-godkänd e-legitimation på tillitsnivå 2, 3
        eller 4 ansluten.

    c.  Att Skolhuvudmannens IDP har egen förmåga att hantera
        signalering enligt DIGG:s definitioner i Sweden Connect eller
        använder en IDP-proxy som har den förmågan. Mer information om
        signalering **här** \[länk till Github\]

    d.  Att Skolhuvudmannens personal vet hur e-legitimationen fungerar
        och används.

2.  IDP-metadata i FIDUS måste deklarera att den egna
    inloggningstjänsten har en direktansluten godkänd e-legitimation.
    Detta deklareras i IDP-metadatat som *Extensions* direkt efter
    elementet *EntityDescriptor*, se exempel;\
    \
    *\<EntityDescriptor xmlns:ds=\"http://www.w3.org/2000/09/xmldsig#\"
    xmlns:saml=\"urn:oasis:names:tc:SAML:2.0:assertion\"
    xmlns:shibmd=\"urn:mace:shibboleth:metadata:1.0\"
    entityID=\"http://idp.exempel.se/\"\>\
    \
    \<Extensions\>\<mdattr:EntityAttributes
    xmlns:mdattr=\"urn:oasis:names:tc:SAML:metadata:attribute\"\>\<saml:Attribute
    Name=\"urn:oasis:names:tc:SAML:attribute:assurance-certification\"
    NameFormat=\"urn:oasis:names:tc:SAML:2.0:attrname-format:uri\"\>\<saml:AttributeValue\>https://fidus.skolverket.se/authentication/e-leg\</saml:AttributeValue\>\</saml:Attribute\>\</mdattr:EntityAttributes\>\
    \</Extensions\>*

3.  Provtjänstens åtkomstgateway kommer i autentiseringsbegäran till IDP
    att skicka en lista med tillitsnivåer (Requested Authentication
    Context) som är godkända att använda. Se exempel på lista;\
    \
    *\<ns0:RequestedAuthnContext Comparison=\"exact\"\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/loa2\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/loa3\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/loa4\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/uncertified-loa2\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/uncertified-loa3\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/loa2-nonresident\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/loa3-nonresident\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/loa4-nonresident\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/nf-low\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/nf-sub\</ns1:AuthnContextClassRef\>
    \<ns1:AuthnContextClassRef\>http://id.elegnamnden.se/loa/1.0/nf-high\</ns1:AuthnContextClassRef\>
    \</ns0:RequestedAuthnContext\>*\
    \
    \
    Efter inloggning med godkänd e-legitimation så svarar IDP:n med den
    tillitsnivå som användes vid inloggningen. Se exempel;\
    \
    *\<saml2:AuthnStatement AuthnInstant=\"2023-09-13T09:54:02Z\"\>
    \<saml2:AuthnContext\>
    \<saml2:AuthnContextClassRef\>http://id.swedenconnect.se/loa/1.0/uncertified-loa2\</saml2:AuthnContextClassRef\>
    \</saml2:AuthnContext\> \</saml2:AuthnStatement\>*\
    \
    **Obs!**\
    En IDP som inte har granskats och godkänts av DIGG ska använda en
    ACCR med prefixet uncertified- när en av DIGG godkänd e-legitimation
    används. Uncertified är alltså att betrakta som normalfallet då
    Skolverket inte kräver att Skolhuvudmannens IDP är granskad, endast
    att e-legitimationen är godkänd.

4.  Genomför ett tekniskt verifieringstest för att se att det fungerar på Skolverkets testtjänst
    **[här](https://fidustest.skolverket.se/DNP/)**
