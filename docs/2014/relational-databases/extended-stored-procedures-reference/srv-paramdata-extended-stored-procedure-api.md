---
title: srv_paramdata(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramdata
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0825b86cabf57df552063335a0870461cb8a5658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127419"
---
# <a name="srv_paramdata-extended-stored-procedure-api"></a>srv_paramdata(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 원격 저장 프로시저 호출 매개 변수의 값을 반환합니다. 이 함수는 **srv_paraminfo** 함수로 대체되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저 호출을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *n*  
 매개 변수의 번호입니다. 첫 번째 매개 변수의 번호는 1입니다.  
  
## <a name="returns"></a>반환 값  
 매개 변수 값에 대한 포인터입니다. *n*번째 매개 변수가 NULL이거나, *n*번째 매개 변수가 없거나, 원격 저장 프로시저가 없으면 NULL이 반환됩니다. 매개 변수 값이 문자열이면 Null로 종결되지 않을 수 있습니다. **srv_paramlen**을 사용하여 문자열 길이를 확인합니다.  
  
 매개 변수가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 중 하나인 경우 이 함수는 다음 값을 반환합니다. 포인터 데이터에는 데이터 형식에 대한 포인터가 유효(VP), NULL 또는 해당 사항 없음(N/A)인지 여부와 가리키는 데이터 콘텐츠가 포함됩니다.  
  
|새 데이터 형식|입력 데이터 길이|  
|--------------------|-----------------------|  
|BITN|**NULL:** VP, NULL<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** 해당 사항 없음<br /><br /> **<255:** 해당 사항 없음|  
|BIGVARCHAR|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** VP, 255자<br /><br /> **<255:** VP, 실제 데이터|  
|BIGCHAR|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, 255개 공백<br /><br /> **>=255:** VP, 255자<br /><br /> **<255:** VP, 실제 데이터 + 패딩(최대 255)|  
|BIGBINARY|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, 255 0x00<br /><br /> **>=255:** VP, 255바이트<br /><br /> **<255:** VP, 실제 데이터 + 패딩(최대 255)|  
|BIGVARBINARY|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, 0x00<br /><br /> **>=255:** VP, 255바이트<br /><br /> **<255:** VP, 실제 데이터|  
|NCHAR|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, 255개 공백<br /><br /> **>=255:** VP, 255자<br /><br /> **<255:** VP, 실제 데이터 + 패딩(최대 255)|  
|NVARCHAR|**NULL:** NULL, N/A<br /><br /> **ZERO:** VP, NULL<br /><br /> **>=255:** VP, 255자<br /><br /> **<255:** VP, 실제 데이터|  
|NTEXT|**NULL:** 해당 사항 없음<br /><br /> **ZERO:** 해당 사항 없음<br /><br /> **>=255:** 해당 사항 없음<br /><br /> **\<255:** 해당 사항 없음|  
  
 \*   데이터가 Null로 종결되지 않으면 255자보다 큰 데이터 잘림에 대한 경고가 표시되지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 매개 변수 이름을 알고 있으면 **srv_paramnumber**를 사용하여 매개 변수 번호를 가져올 수 있습니다. 매개 변수가 NULL인지 여부를 확인하려면 **srv_paramlen**을 사용합니다.  
  
 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 오류가 발생해도 SRV_RPC 처리기는 계속 호출되지만 매개 변수가 없는 것과 같이 처리되며 **srv_rpcparams**는 0을 반환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [srv_rpcparams(확장 저장 프로시저 API)](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
