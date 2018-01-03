---
title: "기본 RDS 프로그래밍 모델 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a206bd1a158b09e3b7041a995bc98351975dfe6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="basic-rds-programming-model"></a>기본 RDS 프로그래밍 모델
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS 주소는 다음과 같은 환경에 존재 하는 응용 프로그램: 클라이언트 응용 프로그램 서버 및 원하는 정보를 반환 하는 데 필요한 매개 변수에서 실행 되는 프로그램을 지정 합니다. 지정 된 데이터 원본에 대 한 서버 향상 액세스에서 호출 프로그램 정보를 검색 하 고, 필요에 따라 해당 데이터를 처리, 쉽게 사용할 수 있는 형태로 클라이언트 응용 프로그램에 결과 정보를 반환 합니다. RDS에는 다음과 같은 일련의 동작을 수행 하는 방법을 제공 합니다.  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트에서 참조 하는 방법을 제공 합니다. (이 참조 라고는 *프록시*합니다. 원격 서버 프로그램을 나타냅니다. 클라이언트 응용 프로그램은 "" 호출할 프록시 로컬 프로그램 되었다가 원격 서버 프로그램을 실제로 호출 하는 경우에 따라.)  
  
-   서버 프로그램을 호출 합니다. 데이터 원본과를 식별 하는 서버 프로그램에 매개 변수를 전달 합니다. (서버 프로그램 실제로 사용 하 여 ADO 데이터 원본에 대 한 액세스 권한을 얻으려고 합니다. ADO 지정된 된 매개 변수 중 하나가 지정 된 연결을 만들고 다른 매개 변수에 지정 된 명령을 발급 합니다.)  
  
-   서버를 얻기는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 데이터 원본의 개체입니다. 필요에 따라는 **레코드 집합** 서버에서 개체를 처리 합니다.  
  
-   서버 프로그램 최종 반환 **레코드 집합** 클라이언트 응용 프로그램에는 개체입니다.  
  
-   클라이언트에서의 **레코드 집합** 개체 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 변환 됩니다.  
  
-   에 대 한 수정을 **레코드 집합** 개체 하는 데이터 소스를 업데이트 하는 데 사용 하는 서버 프로그램 다시 전송 됩니다.  
  
 이 프로그래밍 모델에는 몇 가지 편리한 기능이 포함 되어 있습니다. 데이터 원본에 액세스 하는 복잡 한 서버 프로그램 불필요 하 필요한 연결 및 명령 매개 변수를 제공 하는 경우 RDS가 자동으로 단순, 기본 서버 프로그램을 사용 하 여 지정 된 데이터를 검색 합니다.  
  
 더 복잡 한 처리 해야 하는 경우에 고유의 사용자 지정 서버 프로그램을 지정할 수 있습니다. 예를 들어 사용자 지정 서버 프로그램에 ADO의 모든 기능을 사용 하므로 수 여러 데이터 원본에 연결, 데이터를 일부 복잡 한 방식으로 결합 하 고 클라이언트 응용 프로그램을 간단 하 고 처리 된 결과 반환 합니다.  
  
 마지막으로, 요구 사항 인 위치 사이 ado 기본 서버 프로그램의 동작을 사용자 지정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 프로그래밍 모델 세부 정보](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


