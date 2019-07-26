---
title: '태스크 6: 데이터 흐름에 Excel 원본 추가 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 92a4c3e650ce375a1e80079bbad83c5ab2b9bcd9
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495289"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>태스크 6: Data Flow에 Excel 원본 추가
  이 작업에서는 데이터 흐름에 Excel 원본을 추가하여 원본 Excel 파일에서 공급자 데이터를 읽습니다. Excel 원본은 Microsoft Excel 통합 문서의 워크시트 또는 범위에서 데이터를 추출합니다. 자세한 내용은 [Excel 원본](../integration-services/data-flow/excel-source.md) 항목을 참조하십시오.  
  
1.  **SSIS 도구 상자** 의 **기타 원본** 에서 **데이터 흐름** 탭으로 **Excel 원본** 을 끌어 놓습니다.  
  
2.  **데이터 흐름** 탭에서 **Excel 원본** 을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭합니다.  
  
3.  **Excel 파일에서 공급자 데이터 읽기** 를 입력하고 **Enter**키를 누릅니다.  
  
4.  **Excel 파일에서 공급자 데이터 읽기** 를 두 번 클릭하여 **Excel 원본 편집기** 대화 상자를 시작합니다.  
  
5.  **Excel 원본 편집기** 대화 상자에서 **새로 만들기** 를 클릭하여 Excel 연결을 만듭니다.  
  
6.  **Excel 연결 관리자** 대화 상자에서 **찾아보기**를 클릭하고 **EIM Tutorial** 폴더의 **Suppliers.xls** 파일을 선택합니다. **Excel 버전** 상자에서 **Microsoft Excel 97-2003** 이 선택되어 있는지 확인하고 **확인**을 클릭합니다.  
  
     ![Excel 연결 관리자 대화 상자](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Excel 연결 관리자 대화 상자")  
  
7.  **Excel 원본 편집기** 대화 상자의 **Excel 시트의 이름** 목록 상자에서 **IncomingSuppliers$** 를 선택합니다.  
  
     ![Excel 시트의 이름-들어오는 공급자 $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel 시트의 이름-들어오는 공급자 $")  
  
8.  **미리 보기** 를 클릭하여 Excel 파일의 데이터를 미리 봅니다.  
  
9. **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
10. **SSIS 도구 상자** 의 **기타 변환** 에서 **Excel 파일에서 공급자 데이터 읽기** 아래의 **데이터 흐름** 탭으로 **DQS 정리**를 끌어 놓습니다. DQS 정리 변환에서 기술 자료의 승인된 규칙을 사용하여 DQS(Data Quality Services)로 데이터를 수정합니다. 이 변환은 런타임에 DQS 서버에 DQS 정리 프로젝트를 만듭니다. 자세한 내용은 [DQS 정리 변환](https://msdn.microsoft.com/library/ee677619.aspx) 항목을 참조하십시오.  
  
## <a name="next-step"></a>다음 단계

[작업 7: 데이터 흐름에 DQS 정리 변환 추가](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)  

### <a name="see-also"></a>관련 항목

[데이터 흐름](../integration-services/data-flow/data-flow.md)  
