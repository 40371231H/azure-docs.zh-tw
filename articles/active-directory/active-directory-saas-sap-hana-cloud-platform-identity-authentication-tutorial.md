---
title: "教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: eeb56316b337c90cc83455be11917674eba898a3
ms.openlocfilehash: 9b3f305e71502119e5dee6592347cf30bafef157
ms.contentlocale: zh-tw
ms.lasthandoff: 04/03/2017

---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a>教學課程：Azure Active Directory 與 SAP HANA Cloud Platform Identity Authentication 整合

在本教學課程中，您會了解如何整合 SAP HANA Cloud Platform Identity Authentication 與 Azure Active Directory (Azure AD)。 SAP HANA Cloud Platform Identity Authentication 可做為 Proxy IdP，來存取以 Azure AD 做為主要 IdP 的 SAP 應用程式。

整合 SAP HANA Cloud Platform Identity Authentication 與 Azure AD 提供下列優點：

- 您可以在 Azure AD 中控制可存取 SAP 應用程式的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 SAP 應用程式單一登入 (SSO)
- 您可以在 Azure 傳統入口網站中集中管理您的帳戶

若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。


## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 SAP HANA Cloud Platform Identity Authentication 的整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 SSO 的 **SAP HANA Cloud Platform Identity Authentication** 訂用帳戶


>[!NOTE] 
>若要測試本教學課程中的步驟，我們不建議使用生產環境。
>

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則您不應使用生產環境，。
- 如果您沒有 Azure AD 試用環境，您可以取得[一個月試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。

本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 SAP HANA Cloud Platform Identity Authentication
2. 設定並測試 Azure AD SSO

深入探討技術細節之前，一定要了解您即將查看的概念。 SAP HANA Cloud Platform Identity Authentication 和 Azure Active Directory 同盟可讓您利用 SAP HANA Cloud Platform Identity Authentication 所保護的 SAP 應用程式和服務，跨越 AAD (如 IdP) 所保護的應用程式或服務實作 SSO。

SAP HANA Cloud Platform Identity Authentication 目前做為 SAP 應用程式的領導 Proxy 識別提供者。 而 Azure Active Directory 做為此設定中的識別提供者。 

下圖說明：    

![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

透過此設定，您的 SAP HANA Cloud Platform Identity Authentication 租用戶會設定為 Azure Active Directory 中信任的應用程式。 

接著會在 SAP HANA Cloud Platform Identity Authentication 管理主控台中設定您想透過此方式保護的所有 SAP 應用程式和服務！

這表示對於這類設定 (相對於在 Azure Active Directory 中設定授權)，必須在 SAP HANA Cloud Platform Identity Authentication 中進行授與 SAP 應用程式和服務存取權的授權作業。

透過 Azure Active Directory Marketplace 將 SAP HANA Cloud Platform Identity Authentication 設定為應用程式，您就不需處理所需個別宣告 / SAML 判斷提示和轉換的設定，即可為 SAP 應用程式產生有效的驗證權杖。

>[!NOTE] 
>Web SSO 目前只經過這兩個合作夥伴測試。 應用程式對 API 或 API 對 API 通訊所需的流程應能運作，但尚未經過測試。 它們會在後續活動中進行測試。
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-the-gallery"></a>從資源庫新增 SAP HANA Cloud Platform Identity Authentication
若要設定將 SAP HANA Cloud Platform Identity Authentication 整合到 Azure AD 中，您需要將 SAP HANA Cloud Platform Identity Authentication 從資源庫新增到受管理的 SaaS 應用程式清單中。

**若要從資源庫新增 SAP HANA Cloud Platform Identity Authentication，請執行下列步驟：**

1. 在 [**Azure 管理入口網站**](https://portal.azure.com)的左側瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 按一下對話方塊頂端的 [新增] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **SAP HANA Cloud Platform Identity Authentication**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. 在結果窗格中，選取 [SAP HANA Cloud Platform Identity Authentication]，然後按一下 [新增] 按鈕來新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a>設定和測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SAP HANA Cloud Platform Identity Authentication 設定及測試 Azure AD SSO。

若要讓 SSO 運作，Azure AD 必須知道 SAP HANA Cloud Platform Identity Authentication 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者與 SAP HANA Cloud Platform Identity Authentication 中的相關使用者之間，建立連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中**使用者名稱**的值，指派為 SAP HANA Cloud Platform Identity Authentication 中 **Username** 的值。

若要使用 SAP HANA Cloud Platform Identity Authentication 來設定並測試 Azure AD SSO，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 SAP HANA Cloud Platform Identity Authentication 測試使用者](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - 使 SAP HANA Cloud Platform Identity Authentication 中對應的 Britta Simon 連結到她在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[測試單一登入](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-sso"></a>設定 Azure AD SSO

在本節中，您會在 Azure 管理入口網站中啟用 Azure AD SSO，並在您的 SAP HANA Cloud Platform Identity Authentication 應用程式中設定單一登入。

SAP HANA Cloud Platform Identity Authentication 應用程式需要特定格式的 SAML 判斷提示。 您可以在應用程式整合頁面的 [使用者屬性] 區段中管理這些屬性的值。 以下螢幕擷取畫面顯示上述的範例。

![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

**若要使用 SAP HANA Cloud Platform Identity Authentication 設定 Azure AD SSO，請執行下列步驟：**

1. 在 Azure 管理入口網站的 [SAP HANA Cloud Platform Identity Authentication] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，選取 [SAML 型登入] 做為 [模式]，以啟用單一登入。
 
    ![設定單一登入][5]

3. 在 [單一登入] 對話方塊的 [使用者屬性] 區段中，如果您的 SAP 應用程式預期屬性，例如 "firstName"。 在 [SAML Token 屬性] 對話方塊中新增 "firstName" 屬性。
 1. 按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。
 
    ![設定單一登入][6]

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. 在 [屬性名稱] 文字方塊中，輸入屬性名稱 "firstName"。
 3. 從 [屬性值] 清單選取 "user.givenname" 屬性值。
 4. 按一下 [確定] 。

4. 在 [SAP HANA Cloud Platform Identity Authentication 網域和 URL] 區段上，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. 在 [登入 URL] 文字方塊中，輸入 SAP 應用程式的登入 URL。
 2. 在 [識別碼] 文字方塊中，輸入下列模式的值：`<entity-id>.accounts.ondemand.com` 
    * 如果您不知道此值，請依照[租用戶 SAML 2.0 設定](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html)上的 SAP HANA Cloud Platform Identity Authentication 文件執行。

5. 在 [SAP HANA Cloud Platform Identity Authentication 設定] 區段上，按一下 [設定 SAP HANA Cloud Platform Identity Authentication] 以開啟 [設定登入] 對話方塊。 然後，按一下 [SAML XML 中繼資料] 並將檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. 若要取得為您的應用程式設定的 SSO，請移至 SAP HANA Cloud Platform Identity Authentication 管理主控台。 URL 具有下列模式：`https://<tenant-id>.accounts.ondemand.com/admin`
 * 然後，遵循 SAP HANA Cloud Platform Identity Authentication 文件[將 Microsoft Azure AD 設定成為 SAP HANA Cloud Platform Identity Authentication 的公司識別提供者](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html)。 

7. 在 Azure 管理入口網站中，按一下 [儲存] 按鈕。
8. 只有當您想要為另一個 SAP 應用程式新增和啟用 SSO 時，才繼續以下步驟。 重複＜從資源庫新增 SAP HANA Cloud Platform Identity Authentication＞一節下的步驟，新增另一個 SAP HANA Cloud Platform Identity Authentication 執行個體。
9. 在 Azure 管理入口網站的 [SAP HANA Cloud Platform Identity Authentication] 應用程式整合頁面上，按一下 [連結的登入]。

    ![設定連結的登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. 然後儲存組態。

>[!NOTE] 
>新的應用程式將會利用先前 SAP 應用程式的 SSO 組態。 請確定您在 SAP HANA Cloud Platform Identity Authentication 管理主控台中使用相同的公司識別提供者。
>

### <a name="create-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在新的入口網站中建立名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 管理入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. 移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. 在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。
  2. 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。
  3. 選取 [顯示密碼] 並記下 [密碼] 的值。
  4. 按一下 [建立] 。 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a>建立 SAP HANA Cloud Platform Identity Authentication 測試使用者

您不需要在 SAP HANA Cloud Platform Identity Authentication 上建立使用者。 Azure AD 使用者存放區中的使用者可以使用 SSO 功能。

SAP HANA Cloud Platform Identity Authentication 支援 [識別身分同盟] 選項。 此選項可讓應用程式檢查公司識別提供者所驗證的使用者是否存在於 SAP HANA Cloud Platform Identity Authentication 的使用者存放區中。 

在預設設定中，[識別身分同盟] 選項已停用。 如果已啟用 [識別身分同盟]，則只有匯入 SAP HANA Cloud Platform Identity Authentication 的使用者可以存取應用程式。 

如需如何啟用或停用與 SAP HANA Cloud Platform Identity Authentication 之識別身分同盟的詳細資訊，請參閱[設定與 SAP HANA Cloud Platform Identity Authentication 之使用者存放區的識別身分同盟](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html)中的〈啟用與 SAP HANA Cloud Platform Identity Authentication 的識別身分同盟〉。

### <a name="assign-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您可將 SAP HANA Cloud Platform Identity Authentication 的存取權授予 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 SAP HANA Cloud Platform Identity Authentication，請執行下列步驟：**

1. 在 Azure 管理入口網站中，開啟應用程式檢視，然後瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 **SAP HANA Cloud Platform Identity Authentication**。

    ![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    

### <a name="test-single-sign-on"></a>測試單一登入

在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。

按一下存取面板中的 SAP HANA Cloud Platform Identity Authentication 圖格時，您應該會自動登入 SAP HANA Cloud Platform Identity Authentication 應用程式。


## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png
