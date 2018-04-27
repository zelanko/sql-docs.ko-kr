---
title: 사용자 지정 워크플로 예제(Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: develop
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ded7eed0aae613af59b4eea7b2bc4e892607bc54
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-custom-workflow---example"></a>사용자 지정 워크플로 만들기 - 예제

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]에서 사용자 지정 워크플로 클래스 라이브러리를 만들면 Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender 인터페이스를 구현하는 클래스를 만듭니다. 이 인터페이스에는 워크플로 시작 시 SQL Server MDS Workflow Integration Service가 호출하는 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>라는 메서드가 하나 포함됩니다. <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 메서드에는 두 개의 매개변수가 포함됩니다. *workflowType*에는 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]의 **워크플로 유형** 텍스트 상자에 입력한 텍스트가 들어 있고 *dataElement*에는 워크플로 비즈니스 규칙을 트리거한 항목의 메타데이터와 항목 데이터가 들어 있습니다.  
  
## <a name="custom-workflow-example"></a>사용자 지정 워크플로 예제  
 다음 코드 예제에서는 워크플로 비즈니스 규칙을 트리거한 요소에 대한 XML 데이터에서 Name, Code 및 LastChgUserName 특성을 추출하기 위해 <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> 메서드를 구현하는 방법과 추출한 특성을 다른 데이터베이스에 삽입하기 위한 저장 프로시저를 호출하는 방법을 보여 줍니다. 항목 데이터 XML의 예와 항목 데이터 XML에 포함되는 태그에 대한 설명은 [사용자 지정 워크플로 XML 설명&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)을 참조하십시오.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 워크플로 만들기&#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
