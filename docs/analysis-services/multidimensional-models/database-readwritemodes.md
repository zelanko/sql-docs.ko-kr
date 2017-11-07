---
title: "Readwritemode 데이터베이스 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], read/write
- databases [Analysis Services], read-only
ms.assetid: 03d7cb5c-7ff0-4e15-bcd2-7075d1b0dd69
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 917f9e3802cdf0c003a956b464c7df8d8b10ca5e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="database-readwritemodes"></a>ReadWriteMode 데이터베이스
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA(데이터베이스 관리자)는 읽기/쓰기 데이터베이스를 읽기 전용 데이터베이스로, 또는 이와 반대로 변경해야 하는 경우가 종종 있습니다. 이러한 상황은 솔루션 확장 및 성능 개선을 위해 여러 서버에서 동일한 데이터베이스 폴더를 공유하는 것과 같이 대부분 비즈니스 요구 사항에 의해 발생합니다. 이 경우 **DBA는** ReadWriteMode [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 속성을 사용하여 데이터베이스 운영 모드를 손쉽게 변경할 수 있습니다.  
  
## <a name="readwritemode-database-property"></a>ReadWriteMode 데이터베이스 속성  
 **ReadWriteMode** 데이터베이스 속성은 데이터베이스가 읽기/쓰기 모드에 있는지 또는 읽기 전용 모드에 있는지를 지정합니다. 이 속성 값은 두 가지만 가능합니다. 데이터베이스가 읽기 전용 모드인 경우 변경 사항이나 업데이트 내용을 데이터베이스에 적용할 수 없습니다. 하지만 데이터베이스가 읽기/쓰기 모드인 경우에는 변경 및 업데이트가 가능합니다. **ReadWriteMode** 데이터베이스 속성은 읽기 전용 속성으로 정의되며 **Attach** 명령을 통해서만 설정할 수 있습니다.  
  
 데이터베이스가 읽기 전용 모드인 경우에는 일반적으로 허용되는 데이터베이스 작업 중 일부 작업이 제한됩니다. 제한되는 작업은 다음 표를 참조하십시오.  
  
|읽기 전용 모드|제한되는 작업|  
|-------------------|---------------------------|  
|XML/A 명령<br /><br /> <br /><br /> 참고: 다음 명령 중 하나를 실행하면 오류가 발생합니다.|**만들기**<br /><br /> **Alter**<br /><br /> **Delete**<br /><br /> **처리**<br /><br /> **MergePartitions**<br /><br /> **DesignAggregations**<br /><br /> **CommitTransaction**<br /><br /> **복원**<br /><br /> **동기화**<br /><br /> **Insert**<br /><br /> **Update**<br /><br /> **Drop**<br /><br /> <br /><br /> 참고: 읽기 전용으로 설정된 데이터베이스에서는 셀 쓰기 저장이 가능하지만 변경 내용을 커밋할 수 없습니다.|  
|MDX 문<br /><br /> <br /><br /> 참고: 다음 문 중 하나를 실행하면 오류가 발생합니다.|**COMMIT TRAN**<br /><br /> **CREATE SESSION CUBE**<br /><br /> **ALTER CUBE**<br /><br /> **ALTER DIMENSION**<br /><br /> **CREATE DIMENSION MEMBER**<br /><br /> **DROP DIMENSION MEMBER**<br /><br /> **ALTER DIMENSION**<br /><br /> <br /><br /> 참고: 피벗 테이블 그룹화 기능은 **CREATE SESSION CUBE** 명령을 사용하여 내부적으로 구현되므로 Excel 사용자는 이 기능을 사용할 수 없습니다.|  
|DMX 문<br /><br /> <br /><br /> 참고: 다음 문 중 하나를 실행하면 오류가 발생합니다.|**CREATE [SESSION] MINING STRUCTURE**<br /><br /> **ALTER MINING STRUCTURE**<br /><br /> **DROP MINING STRUCTURE**<br /><br /> **CREATE [SESSION] MINING MODEL**<br /><br /> **DROP MINING MODEL**<br /><br /> **IMPORT**<br /><br /> **SELECT INTO**<br /><br /> **INSERT**<br /><br /> **UPDATE**<br /><br /> **DELETE**|  
|백그라운드 작업|데이터베이스를 수정하는 백그라운드 작업은 사용할 수 없습니다. 여기에는 지연 처리, 자동 관리 캐싱 등이 포함됩니다.|  
  
## <a name="readwritemode-usage"></a>ReadWriteMode 사용법  
 **ReadWriteMode** 데이터베이스 속성은 **Attach** 데이터베이스 명령의 일부로 사용됩니다. **Attach** 명령을 사용하여 데이터베이스 속성을 **ReadWrite** 또는 **ReadOnly**중 하나로 설정할 수 있습니다. **ReadWriteMode** 데이터베이스 속성은 읽기 전용으로 정의되어 있으므로 이 속성 값을 직접 업데이트할 수 없습니다. **ReadWriteMode** 속성이 **ReadWrite**로 설정된 경우에 데이터베이스를 만들 수 있습니다.. 읽기 전용 모드에서는 데이터베이스를 만들 수 없습니다.  
  
 **ReadWriteMode** 데이터베이스 속성을 **ReadWrite** 와 **ReadOnly**간에 전환하려면 **Detach/Attach** 명령 시퀀스를 실행해야 합니다.  
  
 **Attach**를 제외한 모든 데이터베이스 작업은 **ReadWriteMode** 데이터베이스 속성을 현재 상태로 유지합니다. 예를 들어 **Alter**, **Backup**, **Restore**, **Synchronize** 등의 작업은 **ReadWriteMode** 값을 유지합니다.  
  
> [!NOTE]  
>  읽기 전용 데이터베이스에서 로컬 큐브를 만들 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Analysis Services 데이터베이스 이동](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [Detach 요소](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Attach 요소](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  

