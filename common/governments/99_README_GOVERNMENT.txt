




# Government Requirements
# -----------------------
#
# Government authorities and civics use a custom list syntax instead of normal
# triggers in potential and possible to specify valid combinations:
#
#
#	possible = {
#
#		ethics = {
#			# All of these are required:
#			value = ethic_1
#			value = ethic_2
#
#			# One of these is required:
#			OR = {
#				text = translation_key		# optional, overrides the auto-generated tooltip text
#				value = ethic_3
#				value = ethic_4
#			}
#
#			# This one must not be present:
#			NOT = {
#				text = translation_key		# optional
#				value = ethic_5
#				# May contain only one value!
#			}
#
#			# None of these must be present:
#			NOR = {
#				text = translation_key		# optional
#				value = ethic_6
#				value = ethic_7
#			}
#		}
#
#		country_type = { ... }
#
#		authority = { ... }
#
#		civics = { ... }
#
#		# Outer scope is implicitly AND, which means that the result from all specified ethics, country_type, authority or civics blocks must be true
#		# However, it's also possible to add inner OR or AND blocks:
#		OR = {
#			# Only one of these need to be present:
#			authority = { value = my_authority }
#			civics = { value = my_civic }
#
#			# OR/AND blocks can be nested. In this case, that means that if the AND block is fulfilled, the outer OR block will also be fulfilled,
#			# since the OR block only requires one of its constituents to be fulfilled
#			AND = {
#				ethics = { value = ethic_1 }
#				civics = { my_other_civic }
#			}
#		}
#
#		text = translation_key				# optional
#	}
#
#
# Authorities support:
#	- country_type
#	- ethics
#
# Civics support:
#	- country_type
#	- ethics
#	- authority
#	- civics
#
# Species classes support:
#	- country_type
#	- ethics
#	- authority
#	- civics
#
#
#gov_example = {
#	possible = {}							# Determines if a government name can be chosen. AND trigger, scope: country; valid triggers: has_ethic, has_authority, has_valid_civic;
#											# everything else is undefined behavior!
#	weight = {								# scriptable value, scope: country; the (possible) government type with the biggest weight is assigned to the country
#		base = @gov_civic_weight			# Use the standard weight variables depending on if the government is based on an authority, ethic, civic, authority swap, and so on.
#	}										# The weight are found in common\scripted_variables\08_scripted_variables_governments.txt
#											# If multiple civics apply, add a modifer x2 to the weight to elevate it above other similar civic governments.
#											# Civic-based governments have levels of priority, low to high: @gov_civic_weight, @gov_civic_prio_weight, and @gov_civic_override_weight
#											# The weight categories to select a government are (highest selected first):
#											# 1. AI governments
#											# 2. Authority swap governments (except civic_override and galactic sovereign)
#											# 3. Civic governments
#											# 4. Ethic governments
#											# 5. Authority governments
#											# 6. Fallback government
#
#	ruler_title = RT_KING					# translation tag for male ruler's title
#	ruler_title_female = RT_QUEEN			# translation tag for female ruler's title
#	heir_title = HT_CROWN_PRINCE			# translation tag for male heir's title
#	heir_title_female = HT_CROWN_PRINCESS	# translation tag for female heir's title
#	use_regnal_names = yes / no				# default: no
#	dynastic_last_names = yes / no			# default: no
#	should_force_rename = yes / no			# default: no - if set to yes, empires changing to or from this government will be renamed even if authority type does not change
#
#}
