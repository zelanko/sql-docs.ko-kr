---
title: 기본 RDS 프로그래밍 모델 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84b90e2c1338c38538d0c33779fb8e3f5cf2af79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922951"
---
# <a name="basic-rds-programming-model"></a>기본 RDS 프로그래밍 모델
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS 환경에 존재 하는 응용 프로그램을 해결 합니다. 클라이언트 응용 프로그램 서버와 원하는 정보를 반환 하는 데 필요한 매개 변수를 실행 하는 프로그램을 지정 합니다. 지정 된 데이터 원본에 대 한 서버 향상 액세스에서 호출 프로그램 정보를 검색 하 고, 필요에 따라 데이터를 처리, 쉽게 사용할 수 있는 형태로 클라이언트 응용 프로그램에 결과 정보를 반환 합니다. RDS는 다음과 같은 일련의 작업을 수행 하는 방법을 제공 합니다.  
  
-   서버에서 호출 프로그램을 지정 하 고 클라이언트에서 참조 하는 방법을 제공 합니다. (이 참조 라고 한 *프록시*합니다. 원격 서버 프로그램을 나타냅니다. 클라이언트 응용 프로그램은 "call"과 프록시 로컬 프로그램인 있었지만 실제로 원격 서버 프로그램 호출 처럼.)  
  
-   서버 프로그램을 호출 합니다. 데이터 원본 및 실행 하는 명령을 식별 하는 서버 프로그램에 매개 변수를 전달 합니다. (서버 프로그램 실제로 ADO를 사용 하는 데이터 원본에 액세스 합니다. ADO는 지정된 된 매개 변수 중 하나를 사용 하 여 연결 및 다른 매개 변수에서 지정한 명령을 발급 합니다.)  
  
-   서버를 얻기를 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 데이터 원본의 개체입니다. 필요에 따라 합니다 **레코드 집합** 서버의 개체를 처리 합니다.  
  
-   서버 프로그램 반환 최종 **레코드 집합** 클라이언트 응용 프로그램 개체입니다.  
  
-   클라이언트에서의 **레코드 집합** 개체는 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 변환 합니다.  
  
-   수정 된 **레코드 집합** 개체 하는 데이터 소스를 업데이트 하는 데 사용 되는 서버 프로그램 다시 전송 됩니다.  
  
 이 프로그래밍 모델 특정 편의 기능이 포함 되어 있습니다. 데이터 소스에 액세스 하는 복잡 한 서버 프로그램 불필요 하 고 필요한 연결 및 명령 매개 변수를 제공 하는 경우 RDS가 자동으로 간단 하며 기본 서버 프로그램을 사용 하 여 지정된 된 데이터를 검색 합니다.  
  
 더 복잡 한 처리에 필요한 경우 사용자 고유의 사용자 지정 서버 프로그램을 지정할 수 있습니다. 예를 들어, 사용자 지정 서버 프로그램 근거로 활용 ADO 있어서 수 몇 가지 다른 데이터 원본에 연결, 복잡 한 어떤 방식으로든 데이터를 결합 하 고 클라이언트 응용 프로그램을 간단 하 고 처리 결과 반환 합니다.  
  
 마지막으로 요구 조건이 위치 사이 하는 경우 ADO는 이제 기본 서버 프로그램 동작을 사용자 지정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 프로그래밍 모델 세부 정보](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


