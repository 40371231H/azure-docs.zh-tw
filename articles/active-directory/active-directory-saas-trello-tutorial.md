---
title: "教學課程：Azure Active Directory 與 Trello 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Trello 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.translationtype: HT
ms.sourcegitcommit: 2ad539c85e01bc132a8171490a27fd807c8823a4
ms.openlocfilehash: d93667f16f2d72995e4a42e79e9125b8e3f6b07c
ms.contentlocale: zh-tw
ms.lasthandoff: 07/12/2017

---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a>教學課程：Azure Active Directory 與 Trello 整合

在本教學課程中，您將了解如何整合 Trello 與 Azure Active Directory (Azure AD)。

Trello 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Trello 的人員
- 您可以讓使用者利用自己的 Azure AD 帳戶，來自動登入 Trello (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Trello 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Trello 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Trello
2. 設定並測試 Azure AD 單一登入

## <a name="adding-trello-from-the-gallery"></a>從資源庫新增 Trello
如要設定將 Trello 整合到 Azure AD 中，您需要從資源庫把 Trello 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Trello，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Trello**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. 在結果窗格中，選取 [Trello]，然後按一下 [新增] 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Trello 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Trello 與 Azure AD 中互相對應的使用者。 換句話說，必須要建立某位 Azure AD 使用者與 Trello 中相關使用者之間的連結關聯性。

在 Trello 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要設定及測試與 Trello 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Trello 測試使用者](#creating-a-trello-test-user)** - 使 Trello 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Trello 應用程式中設定單一登入。

**若要使用 Trello 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Trello] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. 如果您想要以 **IDP 起始模式**設定應用程式，請在 [Trello 網域和 URL] 區段上執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://trello.com/auth/saml/consume/<enterprise>`

4. 如果您想要以 **SP 起始模式**設定應用程式，請在 [Trello 網域和 URL] 區段上執行下列步驟：
    
    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    a. 按一下 [顯示進階 URL 設定]。

    b.這是另一個 C# 主控台應用程式。 在 [登入 URL] 文字方塊中，以下列模式輸入 URL：`https://trello.com/auth/saml/consume/<enterprise>`

    >[!NOTE]
    >您應該會從 Trello 取得 **\<enterprise\>** slug。 如果您沒有 Slug 值，請連絡 [Trello 支援小組](mailto:support@trello.com)以取得貴企業的 Slug。
    > 

5. Trello 應用程式預期 SAML 判斷提示會包含特定屬性。 設定此應用程式的下列屬性。 您可以從應用程式的 [使用者屬性] 管理這些屬性的值。 以下螢幕擷取畫面顯示上述的範例。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. 在 [SAML Token 屬性]  對話方塊上，針對下表中顯示的每一列執行下列步驟：
 
    | 屬性名稱 | 屬性值 |
    | --- | --- |
    | User.Email | user.mail |
    | User.FirstName | user.givenname |
    | User.LastName | user.surname |

    a. 按一下 [新增屬性] 來開啟 [新增屬性] 對話方塊。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    b. 在 [名稱] 文字方塊中，輸入該資料列所顯示的屬性名稱。 

    c. 在 [值] 清單中，選取該列所顯示的值。
    
    d. 按一下 [確定] 。 
 
7. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. 在 [Trello 組態] 區段上，按一下 [設定 Trello] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. 若要取得為應用程式設定的 SSO，請移至 [Trello 企業 SSO 組態](https://trello.com/sso-configuration) 頁面，將 **SAML 單一登入服務 URL** 傳送給 [Trello 支援小組](mailto:support@trello.com)並附加**憑證 (Base64)**。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-trello-test-user"></a>建立 Trello 測試使用者

在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。 在本節中，您會在 Trello 中建立名為 Britta Simon 的使用者。 Trello 支援即時佈建，而且會在您第一次從 Azure AD 登入時建立新的帳戶。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Trello 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 Trello，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Trello] 。

    ![設定單一登入](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。

當您在存取面板中按一下 Trello 圖格時，應該會自動登入您的 Trello 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png


