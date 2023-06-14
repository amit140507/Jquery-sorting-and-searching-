# Jquery-sorting-and-searching
// js for filter document archive by dropdown and click
var  $window                    = jQuery( window )
            ,$document              = jQuery( this )
            ,$html                      = jQuery( 'html' )
            ,$body                      = jQuery( 'body' )         
            ,curDate                    = new Date()
    ;

    var  $docs = jQuery( '.document' )
                    ,years = [],types = []
                    ,$date_filter = $body.find( '#date-filter' )
            ;

            // Set up sorting data for populating filters
            $docs.each( function() {
                var  year = parseInt( jQuery( this ).attr( 'data-year' ) )
                        ,curYear = curDate.getFullYear()
                        ,type = jQuery( this ).attr( 'data-type' )
                        ,type_id = jQuery( this ).attr( 'data-type-id' )
                ;


                // Check if in current year or last (to prevent empty list on a new year)
                if( year === curYear || year === curYear - 1 ) {
                    jQuery( this ).show();
                }


                if( jQuery.inArray( year,years ) !== -1 ) { /* Not in array */ } else { years.push( year ); }
                if( jQuery.inArray( type,types ) !== -1 ) { /* Not in array */ } else { types.push( type ); }                
            }); 

            // Populate Year Dropdown
            for( y = 0; y < years.length; y++ ) {
                jQuery( '#date-filter' ).append( '<a class="year-option" year-filter="' + years[y] + '">' + years[y] + '</a>' );
            }

                     
            //Filter by Type

            $body.on( 'click','a[rel="filter"]',function() {
                var target = jQuery( this ).attr( 'data-target' );
               // jQuery(this).parent().toggleClass('active');
                // console.log( '.' + target );
                 

                jQuery( '.document' ).hide();
                jQuery('.document').parent().hide();
                // $( '[data-type-id="' + target + '"]' ).show();
                jQuery( '.' + target ).show();
                 jQuery( '.' + target).parent().show();
                // $( '.' + target ).css( 'background-color','lime');
                return false;
            });

            // Filter on Date




                   jQuery('.year-option').on('click', function(){
                    var filter = jQuery( this ).attr('year-filter');
                   // console.log(filter);
                    var datatype = jQuery('.cats-tab').filter('.active').text();
                   // console.log(datatype);
                    if(! filter == '' ) {
                        if(! datatype =='' ){
                            jQuery( '.document' ).hide();
                            jQuery('.document').parent().hide();
                            jQuery( '.document[data-year="' + filter + '"][data-type="' + datatype + '"] ' ).parent().show();
                            jQuery( '.document[data-year="' + filter + '"][data-type="' + datatype + '"] ' ).show();
                        }
                        else
                        {   
                            jQuery( '.document' ).hide();
                            jQuery('.document').parent().hide();
                            jQuery( '.document[data-year="' + filter + '"]' ).parent().show();
                            jQuery( '.document[data-year="' + filter + '"]' ).show();

                        }
                       
                    } 
                    else 
                    {
                        jQuery( '.document' ).parent().show();
                         jQuery( '.document' ).show();
                    }
                    });
