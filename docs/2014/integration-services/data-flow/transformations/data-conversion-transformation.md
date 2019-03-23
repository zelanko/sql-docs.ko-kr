---
title: 데이터 변환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataconversiontrans.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 762bf6b25fec66f5281d32ca9c5d15aa6e64ce31
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374663"
---
# <a name="data-conversion-transformation"></a>데이터 변환
  데이터 변환은 입력 열의 데이터를 다른 데이터 형식으로 변환한 다음 새 출력 열에 복사합니다. 예를 들어 패키지는 여러 개의 원본에서 데이터를 추출한 다음 이 변환을 사용하여 대상 데이터 저장소에 필요한 데이터 형식으로 열을 변환할 수 있습니다. 단일 입력 열에 여러 개의 변환을 적용할 수 있습니다.  
  
 이 변환을 사용하면 패키지가 다음 유형의 데이터 변환을 수행할 수 있습니다.  
  
-   데이터 형식을 변경합니다. 자세한 내용은 [Integration Services Data Types](../integration-services-data-types.md)을 참조하세요.  
  
    > [!NOTE]  
    >  데이터를 날짜 또는 datetime 데이터 형식으로 변환하는 경우 출력 열의 날짜는 로캘 기본 설정에서 다른 형식을 지정해도 ISO 형식으로 표시됩니다.  
  
-   문자열 데이터의 열 길이와 숫자 데이터의 전체 자릿수 및 소수 자릿수를 설정합니다. 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](/sql/t-sql/data-types/precision-scale-and-length-transact-sql)를 참조하세요.  
  
-   코드 페이지를 지정합니다. 자세한 내용은 [Comparing String Data](../comparing-string-data.md)을 참조하세요.  
  
    > [!NOTE]  
    >  문자열 데이터 형식의 열을 다른 문자열 데이터 형식의 열로 복사하는 경우 두 열이 동일한 코드 페이지를 사용해야 합니다.  
  
 문자열 데이터의 출력 열 길이가 해당 입력 열의 길이보다 짧으면 출력 데이터가 잘립니다. 자세한 내용은 [데이터 오류 처리](../error-handling-in-data.md)를 참조하세요.  
  
 이 변환에는 하나의 입력, 하나의 출력 및 하나의 오류 출력이 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다. SSIS 디자이너에서 데이터 변환을 사용하는 방법은 [데이터 변환을 사용하여 데이터를 다른 데이터 형식으로 변환](data-conversion-transformation.md) 및 [데이터 변환 편집기](../../data-conversion-transformation-editor.md)를 참조하세요. 이 변환의 속성을 프로그래밍 방식으로 설정하는 방법은 [공용 속성](../../common-properties.md) 및 [변환 사용자 지정 속성](transformation-custom-properties.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목 - [SSIS 2008의 데이터 형식 변환 기술 간 성능 비교](https://go.microsoft.com/fwlink/?LinkId=220823)  
  
## <a name="see-also"></a>관련 항목  
 [빠른 구문 분석](../../fast-parse.md)   
 [데이터 흐름](../data-flow.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
