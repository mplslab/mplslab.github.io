```java

/**
·*·회원·Controller·Class
·*
·*·@version·:·1.0
·*·@author··:·jsjeon
·*·@date····:·2020.·2.·14.
·*·@see
·*
·*·<pre>
·*·<<·개정이력(Modification·Information)·>>
·*·-----------------------------------------------------------------
·*·····수정일············수정자·················수정내용
·*·-----------------------------------------------------------------
·*···2020.·2.·14.········jsjeon·················MPLS·유지보수·init
·*
·*·</pre>
·*/
@Controller
public·class·UserController
{
····private·static·Log·logger·=·LogFactory.getLog(·UserController.class·);

····/**
·····*·예약정보·등록
·····*
·····*·@version·:·1.0
·····*·@author··:·jsjeon
·····*·@date····:·2020.·2.·24.
·····*
·····*·@param·reserveModel
·····*·@param·rsvNo
·····*·@param·redirectAttributes
·····*·@return
·····*·@throws·Exception
·····*/
····@RequestMapping(value="reserveInit")
····public·@ResponseBody·String·reserveInit(·@ModelAttribute("reserveModel")·ReserveModel·reserveModel,
·············································@RequestParam(value="rsvNo",·required=false)·String·rsvNo,
·············································RedirectAttributes·redirectAttributes·)·throws·Exception
····{
········ResultModel·resultModel·=·new·ResultModel();
········MessageModel·messageModel·=·null;

········if·(·StringUtils.isEmpty(rsvNo))
········{
············try
············{
················/**
·················*·예약정보·등록
·················*/
················rsvNo·=·reserveService.regReserve(·reserveModel·);

················resultModel.setResultCode(Constants.SUCCESS);
············}
············catch(·BusinessException·be·)
············{
················resultModel.setResultCode(Constants.FAIL);
················messageModel·=·be.getMessageModel();
············}
············catch(·Exception·e·)
············{
················log.error(e.getMessage());
············}
········}

········HashMap<String,·Object>·ret·=·new·HashMap<String,·Object>();
········ret.put("messageModel",·messageModel);
········ret.put("result",·······resultModel);
········ret.put("rsvNo",········rsvNo);

········ObjectMapper·mapper·=·new·ObjectMapper();

········return··mapper.writeValueAsString(ret);
····}
}

```