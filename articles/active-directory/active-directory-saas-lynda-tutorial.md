---
title: "教學課程：Azure Active Directory 與 Lynda.com 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lynda.com 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.translationtype: Human Translation
ms.sourcegitcommit: ef1e603ea7759af76db595d95171cdbe1c995598
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.contentlocale: zh-tw
ms.lasthandoff: 06/16/2017


---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a>教學課程：Azure Active Directory 與 Lynda.com 整合

在本教學課程中，您將了解如何整合 Lynda.com 與 Azure Active Directory (Azure AD)。

Lynda.com 與 Azure AD 整合有下列優點：

- 您可以在 Azure AD 中控制可存取 Lynda.com 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lynda.com (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要進行 Azure AD 與 Lynda.com 整合的設定，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Lynda.com 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Lynda.com
2. 設定並測試 Azure AD 單一登入

## <a name="adding-lyndacom-from-the-gallery"></a>從資源庫新增 Lynda.com
若要進行 Lynda.com 與 Azure AD 整合的設定，您需要從資源庫將 Lynda.com 新增至受管理 SaaS 應用程式清單中。

**若要從資源庫新增 Lynda.com，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Lynda.com**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. 在結果面板中，選取 [Lynda.com]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您將以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Lynda.com 搭配運作的 Azure AD 單一登入。

為了讓單一登入正常運作，Azure AD 必須知道 Azure AD 使用者在 Lynda.com 中的對應使用者是誰。 換句話說，必須在 Azure AD 使用者與 Lynda.com 的相關使用者之間建立連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Lynda.com 中 [使用者名稱] 的值。

若要設定及測試與 Lynda.com 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Lynda.com 測試使用者](#creating-a-lyndacom-test-user)** - 使 Lynda.com 中 Britta Simon 的對應使用者連結到該使用者在 Azure AD 中的代表身分。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您將在 Azure 入口網站中啟用 Azure AD 單一登入，並在 Lynda.com 應用程式中設定單一登入。

**若要設定 Lynda.com 的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Lynda.com] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. 在 [Lynda.com 網域及 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `

    > [!NOTE] 
    > 這不是真實的值。 使用實際的登入 URL 來更新此值。 請連絡 [Lynda.com 用戶端支援小組](https://www.linkedin.com/help/lynda/ask)以取得這些值。 
 
4. 在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. 若要在 **Lynda.com** 端設定單一登入，您必須將已下載的**中繼資料 XML** 傳送給 [Lynda.com 支援](https://www.linkedin.com/help/lynda/ask)。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-lyndacom-test-user"></a>建立 Lynda.com 測試使用者

沒有動作項目可讓您設定 Lynda.com 使用者佈建。  
當指派的使用者使用存取面板嘗試登入 Lynda.com 時，Lynda.com 會檢查該使用者是否存在。  

如果尚無可用的使用者帳戶，Lynda.com 會自動予以建立。

>[!NOTE]
>您可以使用 Lynda.com 提供的任何其他 Lynda.com 使用者帳戶建立工具或 API，佈建 AAD 使用者帳戶。 

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您將把 Lynda.com 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 Lynda.com，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Lynda.com]。

    ![設定單一登入](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

如果要測試您的單一登入設定，請開啟存取面板。 如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。 

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png


