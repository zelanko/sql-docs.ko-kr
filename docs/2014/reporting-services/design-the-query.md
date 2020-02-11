---
title: 쿼리 디자인 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f09964013bdc8675e5d4701bd86421317c33fc97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109290"
---
# <a name="design-the-query"></a>쿼리 디자인
  보고서 마법사의 쿼리 디자인 페이지를 사용하여 쿼리를 수동으로 입력하거나 쿼리 작성기에서 대화형으로 쿼리를 작성하거나 다른 보고서에서 쿼리를 가져오는 방법을 통해 쿼리를 만들 수 있습니다.  
  
 보고서 마법사의 이전 페이지인 데이터 원본 선택 페이지에서 선택한 데이터 원본 유형에 따라 이 페이지에 입력할 수 있는 쿼리가 결정됩니다. 예를 들어 데이터 원본 유형이 인 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]경우 문이나 저장 프로시저 이름을 입력할 [!INCLUDE[tsql](../includes/tsql-md.md)] 수 있습니다. 데이터 원본 유형이 인 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]경우 쿼리 창을 사용할 수 없으며 쿼리를 직접 입력할 수 없습니다. 쿼리 작성기를 사용하여 쿼리를 지정할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **쿼리 문자열**  
 보고서에 사용하려는 데이터를 검색할 쿼리를 입력합니다.  
  
 **쿼리 작성기**  
 데이터 원본에 대한 쿼리 디자이너를 열거나 다른 보고서에서 쿼리를 가져오려면 **쿼리 작성기** 를 클릭합니다.  
  
 쿼리 디자이너에 대한 자세한 내용은 [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md)를 참조하십시오.  
  
## <a name="example"></a>예제  
 데이터 원본 유형 **Microsoft SQL Server**의 경우 다음 쿼리는 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스 `Person` 테이블에서 마지막 이름 목록을 검색 합니다.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 데이터 원본 유형 **Microsoft SQL Server**의 경우 다음 쿼리는 id 번호가 1 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 인 직원 `uspGetEmployeeManagers` 에 대해 저장 프로시저를 실행 합니다.  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서 마법사 도움말](../../2014/reporting-services/report-wizard-help.md)   
 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [보고서 &#40;보고서 작성기 및 SSRS&#41;에 데이터를 추가 합니다.](report-data/report-datasets-ssrs.md)  
  
  
