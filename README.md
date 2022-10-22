# ha_templatize_dashboard
Use .yaml templates to more automatically manage Home Assistant Dashboards

Home Assistant gives you the unfortunate choice of an automatically generated "Overview" dashboard, or dashboards that you 
entirely manage yourself. If you manage the dashboard yourself, then you have to add any new entities manually, and the "area"
setting of entities isn't really useful. The automatic "Overview" makes it easy to put entities into areas, but it seems to 
scramble the arrangement of those areas every time you reload it.

In its simplest form, ha_templatize_dashboard lets you take the existing overview, put the areas/rooms in the orientation you 
like, and then easily regenerate your custom dashboard from an updated "Overview" any time you have added new devices and want
them to appear in your well-organized custom dashboard.

It works really well with custom:collapsable-cards, if you don't want all entities shown all the time.

From the --help output:

    usage: ha_templatize_dashboard [-h] [-f FILE] [-s | -t TEMPLATE_FILE] [-J]
                                   [-v] [-w custom:collapsable-cards] [-T] [-H]
    
    yaml templating tool for Home Assistant
    
    optional arguments:
      -h, --help            show this help message and exit
      -f FILE, --file FILE  input "Overview" yaml
      -J, --json            show hierarcy as JSON
      -v, --verbose         give verbose output
      -w custom:collapsable-cards, --wrap custom:collapsable-cards
                            when applying template (-t) wrap each include with,
                            for example, custom:collapsable-cards
      -T, --strip-title     along with --wrap, will strip the title from the
                            included card, leaving only the wrapper card with a
                            title
      -H, --hide-header-toggle
                            when applying template (-t) set
                            show_header_toggle=false on entitites
    
    operation selectors:
      -s, --output-template
                            generate a template file matching the existing
                            overview.yaml input
      -t TEMPLATE_FILE, --template-file TEMPLATE_FILE
                            template file to be expanded
    
    Typical usage:
        (1) Choose an existing dashboard in home assistant which you already have edited, or create 
        a new one with all of your entities (the default).  (You can choose your "Overview" dashboard,
        but realize in step 2 you will be editing it.)
    
        (2) Edit your chosen dashboard to get the complete yaml text of the generated Overview dashboard, 
        and use copy/paste to store it in a file, like overview.yaml.
    
        (3) Then, create a template file, using
        $ ha_templatize_dashboard -f overview.yaml -s >template.yaml
    
        (4) Edit template.yaml to arrange areas and add any additional formatting.
    
        (5) Generate a new dashboard, combining original overview.yaml and template.yaml:
        $ ha_templatize_dashboard -f overview.yaml -t template.yaml >new-overview.yaml
    
        Notes:
        You may not want to re-run step 3 on subsequent generations, after you have made modifications to your
        template. This will keep your previous edits and allow you to discover new entities added to exising areas. 
        New areas won't automatically appear in your template but they are easy to add.
    
        Also, if you do no editing in step 2, then you will just get the default ordering of areas and
        still be able to use the process (skipping step 3) to discover new entities.
    
        To find any new areas, or debug issues with missing "include"s, use -v during step 5 to generate
        comments at the end of the .yaml output.
