---
title: 데이터 원본 속성 대화 상자, 일반 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f918d6583f01473e061792406821b13a4856cea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109483"
---
# <a name="data-source-properties-dialog-box-general"></a>데이터 원본 속성 대화 상자, 일반
  **데이터 원본 속성** 대화 상자의 **일반** 을 선택하여 보고서의 데이터 원본에 대한 연결 정보를 표시하고 수정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 데이터 원본의 이름을 입력합니다. 데이터 원본 이름은 보고서 내에서 중복되지 않아야 합니다. 기본적으로 DataSource1 또는 DataSource2 같은 일반 이름이 데이터 원본에 지정됩니다.  
  
 **포함 된 연결**  
 공유 데이터 원본을 사용하지 않으려면 이 옵션을 선택합니다.  
  
 **형식**  
 데이터 처리 확장 프로그램을 선택합니다. 등록된 확장 프로그램이 목록에 모두 표시됩니다.  
  
 **연결 문자열**  
 데이터 원본에 대한 연결 문자열을 입력합니다. **연결 속성** 대화 상자를 사용하여 연결 문자열을 작성하려면 **편집** 을 클릭합니다. 식을 편집하려면 **식** (*fx*) 단추를 클릭합니다.  
  
 **공유 데이터 원본 참조 사용**  
 공유 데이터 원본에 연결하려면 이 옵션을 선택합니다. 드롭다운 목록에서 공유 데이터 원본을 선택합니다. 선택한 데이터 원본을 편집하려면 **편집**을 클릭합니다. **공유 데이터 원본 참조 사용** 을 선택하면 **유형** 및 **연결 문자열** 이 비활성화됩니다.  
  
 **쿼리 처리 시 단일 트랜잭션 사용**  
 이 데이터 원본을 사용하는 데이터 세트가 데이터베이스에 대해 단일 트랜잭션에서 실행되도록 지정하려면 이 옵션을 선택합니다. 동일한 데이터 원본을 사용하는 하위 보고서에 대한 트랜잭션을 포함하려면 **속성** 창에서 하위 보고서의 **기타** 속성과 관련하여 **MergeTransactions** 를 **True** 로 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [포함 또는 공유 데이터 원본 만들기 &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [데이터 원본 속성 대화 상자, 자격 증명](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
