---
title: 예외 메시지 상자 프로그래밍 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 316afc6d5f3a87ff7431240681066ac5ee66ede6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780701"
---
# <a name="program-exception-message-box"></a>프로그램 예외 메시지 상자
  응용 프로그램에서 예외 메시지 상자를 사용하면 <xref:System.Windows.Forms.MessageBox> 클래스에 비해 메시징 환경을 보다 강력하게 제어할 수 있습니다. 자세한 내용은 [예외 메시지 상자 프로그래밍](../../../2014/database-engine/dev-guide/exception-message-box-programming.md)합니다. 예외 메시지 상자 .dll 가져오기 및 배포에 대한 자세한 내용은 [Deploying an Exception Message Box Application](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md)를 참조하십시오.  
  
## <a name="procedure"></a>프로시저  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>예외 메시지 상자를 사용하여 예외를 처리하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic.NET) 지시어를를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스.  
  
3.  예상되는 예외를 처리할 try-catch 블록을 만듭니다.  
  
4.  `catch` 블록 안에 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다. 전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
5.  (옵션) <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>에 다음 속성 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 예외 메시지 상자에 표시할 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 예외 메시지 상자의 기본 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 예외 메시지 상자의 다른 동작을 제어 하는 데 사용 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 예외 메시지 상자에 표시할 기호를 지정 하는 열거형입니다.  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
7.  (옵션) 사용자가 어느 단추를 클릭했는지 확인하려면 반환된 <xref:System.Windows.Forms.DialogResult> 열거형의 값을 확인합니다.  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>예외 없이 예외 메시지 상자를 표시하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다. 메시지 텍스트를 <xref:System.String> 값으로 전달합니다.  
  
4.  (옵션) <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>에 다음 속성 중 하나 이상을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> 예외 메시지 상자에 표시할 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A> - 예외 메시지 상자의 대화 상자 캡션입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> 예외 메시지 상자의 대화 상자의 기본 단추를 지정 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> 예외 메시지 상자의 다른 동작을 제어 하는 데 사용 하는 열거형입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> 예외 메시지 상자에 표시할 기호를 지정 하는 열거형입니다.  
  
5.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
6.  (옵션) 사용자가 어느 단추를 클릭했는지 확인하려면 반환된 <xref:System.Windows.Forms.DialogResult> 열거형의 값을 확인합니다.  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>사용자 지정된 단추와 함께 예외 메시지 상자를 표시하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  다음의 두 가지 방법 중 하나로 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다.  
  
    -   전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
    -   메시지 텍스트를 <xref:System.String> 값으로 전달합니다.  
  
4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>에 다음 값 중 하나를 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -표시 된 **중단**, **을 다시 시도 하세요**, 및 **무시** 단추.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> - 사용자 지정 단추를 표시합니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -표시 된 **확인** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -표시 된 **확인** 하 고 **취소** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -표시 된 **다시 시도** 및 **취소** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -표시 **예** 하 고 **No** 단추입니다.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -표시 **예**, **아니오**, 및 **취소** 단추입니다.  
  
5.  (옵션) 사용자 지정 단추를 사용할 경우 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> 메서드의 오버로드 중 하나를 호출하여 최대 5개의 사용자 지정 단추에 대해 텍스트를 지정할 수 있습니다.  
  
6.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> 메서드를 호출합니다. 예외 메시지 상자가 속해 있는 부모 창을 전달합니다.  
  
7.  (옵션) 사용자가 어느 단추를 클릭했는지 확인하려면 반환된 <xref:System.Windows.Forms.DialogResult> 열거형의 값을 확인합니다. 사용자 지정 단추를 사용할 경우 사용자가 어느 사용자 지정 단추를 클릭했는지 확인하려면 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> 속성의 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> 값을 확인합니다.  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>예외 메시지 상자의 표시 여부를 사용자가 결정할 수 있게 하려면  
  
1.  관리 코드 프로젝트의 참조를 Microsoft.ExceptionMessageBox.dll 어셈블리에 추가합니다.  
  
2.  (선택 사항) 추가 된 `using` (C#) 또는 `Imports` (Visual Basic.NET) 지시어를 사용 하 여를 <xref:Microsoft.SqlServer.MessageBox> 네임 스페이스입니다.  
  
3.  다음의 두 가지 방법 중 하나로 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> 클래스의 인스턴스를 만듭니다.  
  
    -   전달 된 <xref:System.Exception> 에서 처리 하는 개체를 `try` - `catch` 블록입니다.  
  
    -   메시지 텍스트를 <xref:System.String> 값으로 전달합니다.  
  
4.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> 속성을 `true`으로 설정합니다.  
  
5.  (옵션) 예외 메시지 상자를 다시 표시할지 여부를 사용자에게 묻는 텍스트를 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>에 지정합니다. 기본 텍스트는 "이 메시지를 다시 표시 안 함"입니다.  
  
6.  사용자가 선택한 내용을 응용 프로그램의 실행 기간 동안에만 유지하려면 <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> 값을 전역 <xref:System.Boolean> 변수로 설정합니다. 예외 메시지 상자의 인스턴스를 만들기 전에 이 값을 확인하십시오.  
  
7.  사용자가 선택한 내용을 영구적으로 저장하려면 다음과 같이 합니다.  
  
    1.  CreateSubKey 메서드를 호출하여 응용 프로그램에서 사용하는 사용자 지정 레지스트리 키를 열고, <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A>를 반환되는 CreateSubKey 개체로 설정합니다.  
  
    2.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A>를 사용되는 레지스트리 값의 이름으로 설정합니다.  
  
    3.  <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A>를 `true`로 설정합니다.  
  
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
  
  
