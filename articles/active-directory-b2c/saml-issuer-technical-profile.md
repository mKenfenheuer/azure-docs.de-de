---
title: Definieren eines technischen Profils für einen SAML-Aussteller in einer benutzerdefinierten Richtlinie
titleSuffix: Azure AD B2C
description: Hier erfahren Sie, wie Sie ein technisches Profil für einen SAML-Tokenaussteller (Security Assertion Markup Language) in einer benutzerdefinierten Richtlinie in Azure Active Directory B2C definieren.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 08/17/2020
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: bb5383ee7930cb3d54593f71a709c033d3850889
ms.sourcegitcommit: 023d10b4127f50f301995d44f2b4499cbcffb8fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88521211"
---
# <a name="define-a-technical-profile-for-a-saml-token-issuer-in-an-azure-active-directory-b2c-custom-policy"></a>Definieren eines technischen Profils für einen SAML-Tokenaussteller in einer benutzerdefinierten Richtlinie in Azure Active Directory B2C

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Azure Active Directory B2C (Azure AD B2C) stellt bei der Verarbeitung der einzelnen Authentifizierungsflows verschiedene Arten von Sicherheitstoken aus. Ein technisches Profil für einen SAML-Tokenaussteller gibt ein SAML-Token aus, das an die Anwendung der vertrauenden Seite (Dienstanbieter) zurückgegeben wird. Dieses technische Profil ist in der Regel der letzte Orchestrierungsschritt in der User Journey.

## <a name="protocol"></a>Protocol

Das **Name**-Attribut des **Protocol**-Elements muss auf `None` festgelegt werden. Legen Sie das **OutputTokenFormat**-Element auf `SAML2` fest.

Das folgende Beispiel zeigt ein technisches Profil für `Saml2AssertionIssuer`:

```xml
<TechnicalProfile Id="Saml2AssertionIssuer">
  <DisplayName>Token Issuer</DisplayName>
  <Protocol Name="SAML2"/>
  <OutputTokenFormat>SAML2</OutputTokenFormat>
  <Metadata>
    <Item Key="IssuerUri">https://tenant-name.b2clogin.com/tenant-name.onmicrosoft.com/B2C_1A_signup_signin_SAML</Item>
  </Metadata>
  <CryptographicKeys>
    <Key Id="MetadataSigning" StorageReferenceId="B2C_1A_SamlIdpCert"/>
    <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SamlIdpCert"/>
  </CryptographicKeys>
  <InputClaims/>
  <OutputClaims/>
  <UseTechnicalProfileForSessionManagement ReferenceId="SM-Saml-issuer"/>
</TechnicalProfile>
```

## <a name="input-output-and-persist-claims"></a>Eingabe-, Ausgabe- und Aufbewahrungsansprüche

Die Elemente **InputClaims**, **OutputClaims** und **PersistClaims** sind leer oder fehlen. Die Elemente **InutputClaimsTransformations** und **OutputClaimsTransformations** sind ebenfalls nicht vorhanden.

## <a name="metadata"></a>Metadaten

| attribute | Erforderlich | BESCHREIBUNG |
| --------- | -------- | ----------- |
| IssuerUri | Nein | Der Ausstellername, der in der SAML-Antwort angezeigt wird. Der Wert sollte mit dem Namen übereinstimmen, der in der Anwendung der vertrauenden Seite konfiguriert ist. |
| XmlSignatureAlgorithm | Nein | Die Methode, die Azure AD B2C zur Signierung der SAML-Assertion verwendet. Mögliche Werte: `Sha256`, `Sha384`, `Sha512` oder `Sha1`. Vergewissern Sie sich, dass Sie den Signaturalgorithmus auf beiden Seiten mit demselben Wert konfigurieren. Verwenden Sie nur den Algorithmus, den Ihr Zertifikat unterstützt. Informationen zum Konfigurieren der SAML-Antwort finden Sie unter [SAML-Metadaten der vertrauenden Seite](relyingparty.md#metadata)|

## <a name="cryptographic-keys"></a>Kryptografische Schlüssel

Das CryptographicKeys-Element enthält die folgenden Attribute:

| attribute | Erforderlich | BESCHREIBUNG |
| --------- | -------- | ----------- |
| MetadataSigning | Ja | Das X509-Zertifikat (RSA-Schlüssel) zum Signieren der SAML-Metadaten. Azure AD B2C verwendet diesen Schlüssel zum Signieren der Metadaten. |
| SamlMessageSigning| Ja| Gibt das X509-Zertifikat (RSA-Schlüsselsatz) zum Signieren der SAML-Nachrichten an. Azure AD B2C verwendet diesen Schlüssel zum Signieren der Antwort `<samlp:Response>`, die an die vertrauende Seite gesendet wird.|

## <a name="session-management"></a>Sitzungsverwaltung

Zum Konfigurieren der Azure AD B2C-SAML-Sitzungen zwischen einer Anwendung der vertrauenden Seite, dem Attribut des `UseTechnicalProfileForSessionManagement`-Elements, Verweis auf die [SamlSSOSessionProvider](custom-policy-reference-sso.md#samlssosessionprovider)-SSO-Sitzung.

## <a name="next-steps"></a>Nächste Schritte

Im folgenden Artikel finden Sie ein Beispiel für die Verwendung eines technischen Profils für einen SAML-Aussteller:

- [Registrieren einer SAML-Anwendung in Azure AD B2C](connect-with-saml-service-providers.md)

