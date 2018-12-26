---
title: 예외 메시지 상자 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf02e2759c36ae6408beed0d72b677e130e105a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164113"
---
# <a name="program-exception-message-box"></a>프로그램 예외 메시지 상자
  응용 프로그램 예외 메시지 상자를 사용 하 여에서 제공 하는 것 보다 훨씬 더 많은 메시징 환경 제어를 제공 하는 수 여 <xref:System.Windows.Forms.MessageBox> 클래스입니다. 자세한 내용은 [예외 메시지 상자 프로그래밍](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)합니다. 예외 메시지 상자.dll 가져오기 및 배포 하는 방법에 대 한 정보를 참조 하세요 [예외 메시지 상자 응용 프로그램 배포](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)합니다.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>예외 메시지 상자를 사용하여 예외를 처리하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 지시어를를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스.  
  
3.  예상되는 예외를 처리할 try-catch 블록을 만듭니다.  
  
4.  내 합니다 `catch` 블록에서의 인스턴스를 만듭니다를 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스입니다. 전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
5.  (선택 사항) 다음 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 예외 메시지 상자에 표시할 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 예외 메시지 상자의 기본 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 예외 메시지 상자의 다른 동작을 제어 하는 데 사용 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 예외 메시지 상자에 표시할 기호를 지정 하는 열거형입니다.  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
7.  (선택 사항) 값을 확인 반환 <xref:System.Windows.Forms.DialogResult> 사용자 단추는 확인 해야 할 경우 열거형을 클릭 합니다.  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>예외 없이 예외 메시지 상자를 표시하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다. 메시지 텍스트를 전달 된 <xref:System.String> 값입니다.  
  
4.  (선택 사항) 다음 속성 중 하나 이상을 설정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 예외 메시지 상자에 표시할 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 예외 메시지 상자의 대화 상자 캡션입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 예외 메시지 상자의 대화 상자의 기본 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 예외 메시지 상자의 다른 동작을 제어 하는 데 사용 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 예외 메시지 상자에 표시할 기호를 지정 하는 열거형입니다.  
  
5.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
6.  (선택 사항) 반환된 된 값을 확인 <xref:System.Windows.Forms.DialogResult> 사용자 단추는 확인 해야 할 경우 열거형을 클릭 합니다.  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>사용자 지정된 단추와 함께 예외 메시지 상자를 표시하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  다음의 두 가지 방법 중 하나로 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다.  
  
    -   전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
    -   메시지 텍스트를 전달 된 <xref:System.String> 값입니다.  
  
4.  다음 중 하나에 대 한 값을 설정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -표시 된 **중단**, **을 다시 시도 하세요**, 및 **무시** 단추.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> -사용자 지정 단추를 표시 합니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -표시 된 **확인** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -표시 된 **확인** 하 고 **취소** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -표시 된 **다시 시도** 및 **취소** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -표시 **예** 하 고 **No** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -표시 **예**, **아니오**, 및 **취소** 단추입니다.  
  
5.  (선택 사항) 사용자 지정 단추를 사용 하는 경우의 오버 로드 중 하나를 호출 합니다 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> 최대 5 개의 사용자 지정 단추의 텍스트를 지정 하는 방법입니다.  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
7.  (선택 사항) 반환된 된 값을 확인 <xref:System.Windows.Forms.DialogResult> 사용자 단추는 확인 해야 할 경우 열거형을 클릭 합니다. 사용자 지정 단추를 사용 하는 경우의 값을 적어 둡니다 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> 에 대 한는 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> 속성을 사용자 지정 하는 단추를 클릭 합니다.  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>예외 메시지 상자의 표시 여부를 사용자가 결정할 수 있게 하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  다음의 두 가지 방법 중 하나로 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다.  
  
    -   전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
    -   메시지 텍스트를 전달 된 <xref:System.String> 값입니다.  
  
4.  설정 된 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> 속성을 `true`입니다.  
  
5.  (선택 사항) 텍스트에 예외 메시지 상자의 표시 여부를 결정 하려면 사용자에 게 요청 지정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>합니다. 기본 텍스트는 "이 메시지를 다시 표시 안 함"입니다.  
  
6.  응용 프로그램의 실행 기간에 대해서만 사용자의 결정을 유지 해야 할 경우 값을 설정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> 전역에 <xref:System.Boolean> 변수입니다. 예외 메시지 상자의 인스턴스를 만들기 전에 이 값을 확인하십시오.  
  
7.  사용자가 선택한 내용을 영구적으로 저장하려면 다음과 같이 합니다.  
  
    1.  CreateSubKey 메서드를 호출 응용 프로그램에서 사용 하는 사용자 지정 레지스트리 키를 열고 및 설정 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> 반환 된 RegistryKey 개체입니다.  
  
    2.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A>를 사용되는 레지스트리 값의 이름으로 설정합니다.  
  
    3.  설정할 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> 에 `true`입니다.  
  
    4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 지정된 레지스트리 키가 확인되고, 레지스트리 키에 저장된 데이터가 0인 경우에만 예외 메시지 상자가 표시됩니다. 대화 상자가 표시되고 사용자가 단추를 클릭하기 전에 확인란을 선택하면 레지스트리 키의 데이터가 1로 설정됩니다.  
  
## <a name="example"></a>예제  
 이 예에서는 **확인** 단추만 있는 예외 메시지 상자를 사용하여 처리된 예외 및 추가적인 애플리케이션 관련 정보가 포함된 애플리케이션 예외 정보를 표시합니다.  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>예제  
 이 예에서는 사용자가 선택할 수 있는 **예** 및 **아니요** 단추가 포함된 예외 메시지 상자를 사용합니다.  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>예제  
 이 예에서는 사용자 지정 단추가 포함된 예외 메시지 상자를 사용합니다.  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>예제  
 이 예에서는 확인란을 사용하여 예외 메시지 상자의 표시 여부를 결정합니다.  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>예제  
 이 예에서는 확인란과 레지스트리 키를 사용하여 예외 메시지 상자의 표시 여부를 결정합니다.  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>예제  
 이 예에서는 예외 메시지 상자를 사용하여 문제 해결이나 디버깅에 도움이 되는 추가적인 정보를 표시합니다.  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
