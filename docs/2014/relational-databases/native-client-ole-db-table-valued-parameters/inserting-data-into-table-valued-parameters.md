---
title: 테이블 반환 매개 변수에 데이터 삽입 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
ms.assetid: 9c1a3234-4675-40d3-b473-8df06208f880
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71cd369568d8fc66764345038568818a551f9fb3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48093843"
---
# <a name="inserting-data-into-table-valued-parameters"></a>테이블 반환 매개 변수에 데이터 삽입
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 테이블 반환 매개 변수 행에 대 한 데이터를 지정 하는 두 가지 모델을 지원 합니다: 밀어넣기 모델과 끌어오기 모델입니다. 끌어오기 모델을 보여 주는 예제를 사용할 수 있습니다. [SQL Server 데이터 프로그래밍 예제](http://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
> [!NOTE]  
>  테이블 반환 매개 변수 열은 모든 행에 기본값이 아닌 값이 있거나 모든 행에 기본값이 있어야 합니다. 일부 행에만 기본값이 있으면 안 됩니다. 따라서 테이블 반환 매개 변수 바인딩에서 테이블 반환 매개 변수 행 집합 열 데이터에는 DBSTATUS_S_ISNULL 및 DBSTATUS_S_OK 상태 값만 사용할 수 있습니다. DBSTATUS_S_DEFAULT를 사용하면 오류가 발생하며 바인딩 상태 값은 DBSTATUS_E_BADSTATUS로 설정됩니다.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>밀어넣기 모델(모든 테이블 반환 매개 변수 데이터를 메모리에 로드)  
 밀어넣기 모델은 매개 변수 집합(ICommand::Execute의 DBPARAMS 매개 변수)을 사용하는 것과 비슷합니다. 테이블 반환 매개 변수 행 집합 개체가 IRowset 인터페이스의 사용자 지정된 구현 없이 사용되는 경우에만 밀어넣기 모델이 사용됩니다. 밀어넣기 모델은 테이블 반환 매개 변수 행 집합의 행 수가 적어 응용 프로그램에 과도한 메모리 부담을 주지 않는 경우에만 사용하는 것이 좋습니다. 이 모델은 현재 일반적인 OLE DB 응용 프로그램에서 흔히 사용되는 기능 이외의 기능은 소비자 응용 프로그램에 요구하지 않기 때문에 끌어오기 모델보다 간단합니다.  
  
 소비자는 명령을 실행하기 전에 모든 테이블 반환 매개 변수 데이터를 공급자에게 제공해야 합니다. 데이터를 제공하기 위해 소비자는 각 테이블 반환 매개 변수의 테이블 반환 매개 변수 행 집합 개체를 채웁니다. 테이블 반환 매개 변수 행 집합 개체는 행 집합 삽입, 설정 및 삭제 작업을 제공하며, 소비자는 이를 사용하여 테이블 반환 매개 변수 데이터를 조작합니다. 공급자는 실행 시에 이 테이블 반환 매개 변수 행 집합 개체에서 데이터를 인출합니다.  
  
 테이블 반환 매개 변수 행 집합 개체가 소비자에 제공되면 소비자는 이를 행 집합 개체로 처리할 수 있습니다. Icolumnsinfo:: Getcolumninfo 또는 icolumnsrowset:: Getcolumnsrowset 인터페이스 메서드를 사용 하 여 소비자 (형식, 최대 길이, 전체 자릿수 및 소수) 각 열의 형식 정보를 가져올 수 있습니다. 그런 다음 소비자는 데이터에 대한 바인딩을 지정하기 위한 접근자를 만듭니다. 다음 단계는 데이터의 행을 테이블 반환 매개 변수 행 집합에 삽입하는 것입니다. Irowsetchange:: Insertrow를 사용 하 여이 수행할 수 있습니다. Irowsetchange:: Setdata 또는 irowsetchange:: Deleterows 데이터를 조작 해야 할 경우 테이블 반환 매개 변수 행 집합 개체에도 사용 수 있습니다. 테이블 반환 매개 변수 행 집합 개체는 스트림 개체와 비슷하게 참조 횟수가 계산됩니다.  
  
 Icolumnsrowset:: Getcolumnsrowset 사용 되는 경우 irowset:: Getnextrows, irowset:: Getdata를 및 irowset:: Releaserows 메서드 결과 열의 행 집합 개체에 대 한 후속 호출 됩니다.  
  
 이후에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 시작 하는 명령을 실행, 테이블 반환 매개 변수 값이 테이블 반환 매개 변수 행 집합 개체에서 인출 되어 서버로 전송 합니다.  
  
 밀어넣기 모델에서는 필요한 소비자 작업이 최소화되지만 실행 시 모든 테이블 반환 매개 변수 데이터가 메모리 내에 있어야 하므로 끌어오기 모델에 비해 더 많은 메모리가 사용됩니다.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>끌어오기 모델(요청 시 소비자로부터 테이블 반환 매개 변수 데이터를 가져옴)  
 끌어오기 모델은 다음과 같은 두 가지 경우에 유용합니다.  
  
-   행을 스트리밍하려는 경우  
  
-   다른 공급자의 행 집합이 테이블 반환 매개 변수 값으로 사용되는 경우.  
  
 끌어오기 모델에서는 소비자가 공급자에게 데이터를 요청 시 제공합니다. 응용 프로그램에 데이터 삽입 내용이 많고, 메모리의 테이블 반환 매개 변수 행 집합 데이터로 인해 과도한 메모리 액세스가 발생할 가능성이 높은 경우 이 방법을 사용하십시오. 여러 OLE DB 공급자가 사용되는 경우 소비자 끌어오기 모델을 통해 소비자는 모든 행 집합 개체를 테이블 반환 매개 변수 값으로 제공할 수 있습니다.  
  
 끌어오기 모델을 사용하려면 소비자는 행 집합 개체의 자체 구현을 제공해야 합니다. 소비자는 공급자는 ITableDefinitionWithConstraints 통해 노출 되는 테이블 반환 매개 변수 행 집합 개체를 집계 하는 데 필요한 테이블 반환 매개 변수 행 집합 (CLSID_ROWSET_TVP)를 사용 하 여 끌어오기 모델을 사용 하는 경우: CreateTableWithConstraints 메서드나 iopenrowset:: Openrowset 메서드 소비자 개체는 IRowset 인터페이스 구현만 재정의해야 합니다. 다음 함수는 사용자가 재정의해야 합니다.  
  
-   IRowset::GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset::GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset::RestartPosition  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 소비자 행 집합 개체에서 한 번에 하나 이상의 행을 읽어 테이블 반환 매개 변수의 스트리밍 동작을 지원합니다. 예를 들어 사용자의 테이블 반환 매개 변수 행 집합 데이터가 메모리가 아닌 디스크에 있고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 해당 데이터를 요구하는 경우 사용자가 디스크에서 데이터를 읽는 기능을 구현할 수 있습니다.  
  
 소비자는 해당 데이터 형식을 통신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 테이블 반환 매개 변수 행 집합 개체에서 iaccessor:: Createaccessor를 사용 하 여 합니다. 공급자는 소비자 버퍼에서 데이터를 읽을 때 최소한 하나의 접근자 핸들을 통해 쓰기 가능하고 기본 열이 아닌 모든 열을 사용할 수 있는지 확인하고, 해당 핸들을 사용하여 열 데이터를 읽습니다. 모호성을 피하려면 테이블 반환 매개 변수 행 집합 열과 바인딩이 일 대 일로 대응해야 합니다. 동일한 열에 대한 중복 바인딩은 오류를 일으킵니다. 각 접근자 것으로 예상 되는 또한 합니다 *iOrdinal* 순서로 DBBindings의 멤버입니다. IRowset::GetData는 행당 접근자 수만큼 호출되며 *iOrdinal* 값을 기반으로 낮은 값에서 높은 값 순서로 호출됩니다.  
  
 공급자는 테이블 반환 매개 변수 행 집합 개체에 의해 제공되는 인터페이스의 대부분을 구현해야 합니다. 소비자는 최소한의 인터페이스(IRowset)로 행 집합 개체를 구현합니다. 무계획적인 집계로 인해 남은 필수 행 집합 개체 인터페이스는 테이블 반환 매개 변수 행 집합 개체에 의해 구현됩니다.  
  
 OLE DB 공급자에 대해 가져온 행 집합 개체를 비롯한 다른 모든 행 집합 개체의 경우 소비자가 제공한 행 집합은 OLE DB 사양에 지정된 대로 모든 필수 행 집합 개체 인터페이스를 구현해야 합니다.  
  
 실행 시점에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 행 집합 개체를 호출하여 행을 인출하고 열 데이터를 읽습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블 반환 매개 변수&#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
