---
title: 스크립트 태스크에서 결과 반환 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cfc772b9809327e9b5383e81f489b5cf390f28ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620561"
---
# <a name="returning-results-from-the-script-task"></a>스크립트 태스크에서 결과 반환
  스크립트 태스크에서는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>와 선택적 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 속성을 사용하여 스크립트 태스크가 완료된 후 워크플로의 경로를 확인하는 데 사용할 수 있는 상태 정보를 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임에 반환합니다.  
  
## <a name="taskresult"></a>TaskResult  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> 속성은 태스크가 성공했는지 여부를 보고합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 속성은 선택적으로 스크립트 태스크의 성공 여부에 대한 추가 정보를 수량화하거나 제공하는 사용자 정의 개체를 반환합니다. 예를 들어 FTP 태스크는 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> 속성을 사용하여 전송된 파일 수를 반환하고, SQL 실행 태스크는 태스크의 영향을 받은 행 수를 반환합니다. <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>를 사용하여 워크플로의 경로를 확인할 수도 있습니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
