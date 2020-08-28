---
description: 기본 RDS 프로그래밍 모델
title: 기본 RDS 프로그래밍 모델 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
author: rothja
ms.author: jroth
ms.openlocfilehash: a943c8b4f42dc5ca232114070e5e09ac318889d0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978384"
---
# <a name="basic-rds-programming-model"></a>기본 RDS 프로그래밍 모델
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 RDS는 다음 환경에 있는 응용 프로그램을 해결 합니다. 클라이언트 응용 프로그램은 서버에서 실행 되는 프로그램 및 원하는 정보를 반환 하는 데 필요한 매개 변수를 지정 합니다. 서버에서 호출 된 프로그램은 지정 된 데이터 원본에 대 한 액세스 권한을 획득 하 고, 정보를 검색 하 고, 필요에 따라 데이터를 처리 한 다음, 쉽게 사용할 수 있는 형태로 클라이언트 응용 프로그램에 결과 정보를 반환 합니다. RDS는 다음과 같은 일련의 작업을 수행할 수 있는 방법을 제공 합니다.  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트에서이를 참조 하는 방법을 가져옵니다. 이 참조를 *프록시*라고도 합니다. 원격 서버 프로그램을 나타냅니다. 클라이언트 응용 프로그램은 로컬 프로그램인 것 처럼 프록시를 "호출" 하지만 실제로는 원격 서버 프로그램을 호출 합니다.  
  
-   서버 프로그램을 호출 합니다. 데이터 원본 및 실행할 명령을 식별 하는 서버 프로그램에 매개 변수를 전달 합니다. 서버 프로그램은 실제로 ADO를 사용 하 여 데이터 원본에 대 한 액세스 권한을 얻습니다. ADO는 지정 된 매개 변수 중 하 나와 연결 하 고 다른 매개 변수에 지정 된 명령을 실행 합니다.  
  
-   서버 프로그램은 데이터 원본에서 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 가져옵니다. 필요에 따라 **레코드 집합** 개체가 서버에서 처리 됩니다.  
  
-   서버 프로그램은 최종 **레코드 집합** 개체를 클라이언트 응용 프로그램으로 반환 합니다.  
  
-   클라이언트에서 **레코드 집합** 개체는 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 저장 됩니다.  
  
-   **레코드 집합** 개체에 대 한 수정 내용은 서버 프로그램으로 다시 전송 되며이 프로그램을 사용 하 여 데이터 원본을 업데이트 합니다.  
  
 이 프로그래밍 모델은 편리한 특정 기능을 포함 합니다. 데이터 원본에 액세스 하는 데 복잡 한 서버 프로그램이 필요 하지 않고 필요한 연결 및 명령 매개 변수를 제공 하는 경우 RDS는 간단한 기본 서버 프로그램을 사용 하 여 지정 된 데이터를 자동으로 검색 합니다.  
  
 더 복잡 한 처리가 필요한 경우 고유한 사용자 지정 서버 프로그램을 지정할 수 있습니다. 예를 들어 사용자 지정 서버 프로그램은 ADO의 모든 기능을 사용할 수 있기 때문에 다양 한 데이터 원본에 연결 하 고, 데이터를 몇 가지 복잡 한 방식으로 결합 하 고, 처리 된 간단한 결과를 클라이언트 응용 프로그램에 반환할 수 있습니다.  
  
 마지막으로, 사용자의 요구가의 어딘가에 있는 경우 ADO는 이제 기본 서버 프로그램의 동작을 사용자 지정 하도록 지원 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 프로그래밍 모델 세부 정보](./rds-programming-model-in-detail.md)   
 [RDS 시나리오](./rds-scenario.md)   
 [RDS 자습서](./rds-tutorial.md)   
 [레코드 집합 개체 (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [RDS 사용량 및 보안](./rds-usage-and-security.md)