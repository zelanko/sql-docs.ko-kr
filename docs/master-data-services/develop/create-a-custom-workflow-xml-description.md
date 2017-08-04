---
title: "사용자 지정 워크플로 XML 설명 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ca6f208bab4ed0b7932d3bd5f7e9a911b8b2c8af
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---xml-description"></a>-사용자 지정 워크플로 XML 설명 만들기
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]에서 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 메서드는 워크플로 시작 시 SQL Server MDS Workflow Integration Service가 호출합니다. 이 메서드는 워크플로 비즈니스 규칙을 트리거한 항목에 대한 메타데이터 및 데이터를 XML 블록으로 받습니다. 예를 들어 워크플로 처리기를 구현 하는 코드 참조 [사용자 지정 워크플로 예제 &#40; Master Data services&#41; ](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 다음 예제에서는 워크플로 처리기로 전송되는 XML을 보여 줍니다.  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 다음 표에서는 이 XML에 포함되는 태그 일부에 대해 설명합니다.  
  
|태그|Description|  
|---------|-----------------|  
|\<유형 >|에 입력 한 텍스트는 **워크플로 유형** 텍스트 상자에 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 로드 하는 사용자 지정 워크플로 어셈블리를 식별 하 합니다.|  
|\<SendData >|에 의해 제어 되는 부울 값은 **메시지에 멤버 데이터 포함** 확인란을 선택 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]합니다. 즉 값 1은 \<MemberData > 섹션 전송 되 고,는 \<MemberData > 섹션이 전송 되지 않습니다.|  
|< Server_URL >|에 입력 한 텍스트는 **워크플로 사이트** 텍스트 상자에 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]합니다.|  
|< Action_ID >|에 입력 한 텍스트는 **워크플로 이름을** 텍스트 상자에 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]합니다.|  
|\<MemberData >|워크플로 동작을 트리거한 멤버의 데이터를 포함합니다. 경우에 포함 되는지 값 \<SendData >는 1입니다.|  
|\<입력*xxx*>|이 태그 집합에는 멤버 생성에 대한 메타데이터(예: 만든 날짜, 만든 사람 등)가 포함됩니다.|  
|\<LastChg*xxx*>|이 태그 집합에는 멤버에 적용된 마지막 변경 내용에 대한 메타데이터(예: 변경 내용을 적용한 날짜, 변경 내용을 적용한 사람 등)가 포함됩니다.|  
|\<이름 >|변경된 멤버의 첫 번째 특성입니다. 이 예제 멤버에는 Name 및 Code 특성만 포함되어 있습니다.|  
|\<코드 >|변경된 멤버의 다음 특성입니다. 이 예제 멤버에 더 많은 특성이 포함될 경우 해당 특성은 이 특성 다음에 오게 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 워크플로 &#40; 만들기 Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)   
 [사용자 지정 워크플로 예제 &#40; Master Data services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)  
  
  
