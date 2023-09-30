#  First Contact
#  -----------------------
#
#  The First Contact process starts whenever two empires meet for the first time. 
#  Like espionage operations and archeological sites, first contact sites are split in stages, each with a difficulty level and a resulting event. 
#
#  Sometimes you DON'T want a first contact process to fire - like when you're spawning an empire just to have a single ship/leader to use in an event.
#  In such cases, you can define whether a particular country type can start First Contact or not by editing the EFFECT can_have_first_contact in game_rules/00_rules.txt.
#
#
#  FIRST CONTACT SITES
#  -----------------------
#  First Contact sites are assigned depending on empire country type.
#  Every time you meet a new empire, base_contact_set is fired, which then fires first_contact.1: the default "encounter in X system" event. 
#  The event then fires the SCRIPTED EFFECT set_first_contact_starting_stage, checking the country type and assigning the right site to the empire
#  depending on the country type.
#
#  Default empires have a handful of somewhat randomized, generic First Contact sites (defined in 00_first_contact.txt). Critters and enclaves have
#  their own personalized chains (defined in 01_first_contact_space_fauna_and_NPCs.txt)
#
#
#  ADDING NEW UNIQUE FIRST CONTACT STORIES
#  -----------------------
#  By default, base_contact_set fires EVENT first_contact.1 - the generic "encounter in X system" event that is common
#  for every new encounter. If you are planning to use First Contact to write more unique stories, you can fire an alternate event instead.
#  An example is the "Dragon Communications Study" in the Here Be Dragons Origin, where you are trying to communicate with the
#  giant dragon roaming in your system. 
#  You fire the alternate event by adding an exception to base_contact_set:
#
#  stage_event = {
# 	summary = "your_loc_string"					# To be displayed in the stage icon tooltip in the first contact interface
# 	event_weight = {
# 		weight = 0
# 		modifier = {
# 			weight = 1000
# 			from = {
# 				is_country_type = dragon_dummy	# The condition that will be tested to decide whether to fire the
# 			}									# alternate event. Usually checked against country type, but you can
# 		}										# use whatever.
# 	}
# 	event = first_contact.XXXX					# the ID of the event to be fired
#  }
#
#  Start to create your new event by using first_contact.1 as a reference.
#  After that, edit the SCRIPTED EFFECT set_first_contact_starting_stage, adding your new empire type:
#
#  <country_type> = { setup_first_contact_path = { TYPE = <stage_name> } }
#
#  Example: 
#
#  drone_faction = { setup_first_contact_path = { TYPE = drones } }
#
#
#  EXAMPLE
#  -----------------------
#
#  void_clouds_stage_1 = {
# 	icon = <sprite key>							# Stage icon (from game/interface/first_contact_view.gfx)
# 	picture = <sprite key>						# Event picture associated with the stage
#
# 	difficulty = <int>							# Difficulty level
#
# 	stage_event = {								# The event that will trigger once the stage succeeds. It's possible to set
# 												# multiple stage_event and use weights and modifiers to randomize the chosen event.
# 		summary = <string>						# Summary of the current stage
# 		event_weight = {						# Default event weight
# 			weight = X
# 			modifier = {						# (Optional) weight modifiers.
# 				weight = X						# Only used to randomize events when multiple stage_event are se
# 				(trigger conditions)
# 			}
# 		}
# 		event = <event ID>						# ID of the event to be fired
# 	}
#
# 	on_roll_failed = {
# 		standard_first_contact_on_roll_failed = { RANDOM_EVENTS = <random_list> } # random list of negative events to fire. Defined in first_contact_effects
# 	}
#  }
