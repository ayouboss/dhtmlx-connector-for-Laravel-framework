DHTMLX Connector for Laravel framework
======================================

This is the module to integrate [DHTMLX PHP Connector] to the [Laravel] framework. 

####Controller

```sh
<?php

require_once("../public/codebase/connector/scheduler_connector.php");
require_once("../public/codebase/connector/db_phplaravel.php");


class DhtmlxConnectorController extends BaseController {

    /**
     * Event Model
     * @var Event
     */
    protected $events;


    /**
     * Inject the models.
     * @param Event $events
    
     */
    public function __construct(Event $events)
    {
        parent::__construct();

        $this->event = $events;
      
    }
    
	/**
	 * Draws the scheduler.
	 *
	 * @return View
	 */
	public function getIndex()
	{
		return View::make('scheduler/index');
	}
	/**
	 * Loads all events.
	 *
	 * @return events
	 */
	public function load(){                                               

		

		$connector = new SchedulerConnector($this->event,"PHPLaravel");               
        $connector->configure("events","id","start_date,end_date,event_name");
        $connector->render();                                                       
    }
	/**
	 * Saves events.
	 *
	 * @return events
	 */
	public function save(){                                               
														
        $connector = new SchedulerConnector($this->event, "PHPLaravel");               
        $connector->configure("events","id","start_date,end_date,event_name");
        $connector->render();                                                       
    }
	
}
```

###Model
```sh
<?php



class Event extends Eloquent{


}
```
###View
```sh
<!DOCTYPE html>
<head>
	<meta http-equiv="Content-type" content="text/html; charset=utf-8">
	<title>Basic initialization</title>
</head>
	<script src="codebase/dhtmlxscheduler.js" type="text/javascript" charset="utf-8"></script>

	<link rel="stylesheet" href="codebase/dhtmlxscheduler_flat.css" type="text/css" media="screen" title="no title" charset="utf-8">

	
<style type="text/css" media="screen">
	html, body{
		margin:0px;
		padding:0px;
		height:100%;
		overflow:hidden;
	}
</style>

<script type="text/javascript" charset="utf-8">
	function init() {
	
		scheduler.config.xml_date="%Y-%m-%d %H:%i:%s";
		

		scheduler.init('scheduler_here',new Date(),"week");

		scheduler.load("./scheduler/load");
		
		var dp = new dataProcessor("./scheduler/save");
		dp.setTransactionMode("POST");
		dp.init(scheduler);

		}
</script>

<body onload="init();">
<div id="scheduler_here" class="dhx_cal_container" style='width:100%; height:100%;'>
		<div class="dhx_cal_navline">
			<div class="dhx_cal_prev_button">&nbsp;</div>
			<div class="dhx_cal_next_button">&nbsp;</div>
			<div class="dhx_cal_today_button"></div>
			<div class="dhx_cal_date"></div>
			<div class="dhx_cal_tab" name="day_tab" style="right:204px;"></div>
			<div class="dhx_cal_tab" name="week_tab" style="right:140px;"></div>
			<div class="dhx_cal_tab" name="month_tab" style="right:76px;"></div>
		</div>
		<div class="dhx_cal_header">
		</div>
		<div class="dhx_cal_data">
		</div>		
	</div>
</body>
```
**CSRF Filter should be disabled**





[dhtmlx php connector]:http://docs.dhtmlx.com/connector__php__index.html
[laravel]:http://laravel.com
