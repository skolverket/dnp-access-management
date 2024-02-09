**Checklista för inloggning med egen IDP och eduID som
e-legitimation**

1.  Grundförutsättningar för att inloggning med eduID som e-legitimation
    ska fungera är;

    a.  Inloggning med egen IDP utan e-legitimation fungerar enligt checklista och tekniskt verifieringstest

    b.  Att Skolhuvudmannen beställt eduID som e-legitimation via
        Skolverkets e-tjänst Administration provtjänsten
    
    c.  Att Skolhuvudmannens personal innehar ett eduID-konto och
        anslutit en säkerhetsnyckel\*

    d.  Att Skolhuvudmannen via Skolverkets provisioneringstjänst
        provisionerat en id-länkning mellan personalens EPPN och deras
        eduID-EPPN\
        \
        **OBS!**\
        Utan en korrekt id-länkning kommer inte eduID som e-legitimation att
        påföras inloggningen när e-legitimation krävs och personalen då inte
        få åtkomst till provtjänsten.

3.  Genomför ett tekniskt verifieringstest för att se att det fungerar på Skolverkets testtjänst
    **[här](https://fidustest.skolverket.se/DNP/)**


**\* Notera följande angående säkerhetsnyckeln:**

Följande krav ställs på säkerhetsnyckeln som används tillsammans med eduID som e-legitimation för att den ska vara godkänd av DIGG på tillitsnivå 2:
 
1. Säkerhetsnyckeln ska vara certifierad för FIDO2 (fidoalliance.org)
2. Säkerhetsnyckeln ska i samband med inloggning ställa ut ett intyg utfärdat av tillverkaren som berättar vilken enhet det är och kräva att personen är fysiskt vid säkerhetsnyckeln för att den ska kunna användas. 
 
Notera att alla FIDO2-certifierade produkter inte lever upp till krav nr 2 så kontrollera att detta uppfylls med tillverkaren eller återförsäljaren. 
