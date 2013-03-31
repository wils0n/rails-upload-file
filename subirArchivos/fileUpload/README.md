##Subiendo Archivos
En esta app se ha usado la gema 'carrierwave' que nos proporciona una forma simple y flexible de cargar archivos desde aplicacioens Rails.
###Uso:
Instalar la gema (agregar, luego bundle)

	gem 'carrierwave'

Generar una clase qeu gestionará las subidas (image es la clase)

	$ rails g uploader image

Agregar esta clase al modelo con el cual estas trabajando
	
	$ rails g migration add_image_to_pictures image:string
	$ rake db:migrate

Vincular la clase con el modelo Picture llamando al método  mount_uploader pasandole el nombre de la columna generada anteriormente. Tambien agregar la columna image a la lista attr_accessible para poder acceder

	class Picture < ActiveRecord::Base
	  attr_accessible :name, :image
	  mount_uploader :image, ImageUploader
	end

Modificar el formulario para que gestione la subida de archivos

	<%= form_for @picture, :html => {:multipart => true} do |f| %>

[Mayor informacion](https://github.com/jnicklas/carrierwave).

***Observaciones
-Las imagenes se cargan por defecto a la carpeta public/uploads/pictures, esta se puede cambiar con:
	
	class MyUploader < CarrierWave::Uploader::Base
	  def store_dir
	    'public/my/upload/directory'
	  end
	end

-Si bien es cierto las gemas 'carrierwave', 'rmagick'
tienen sus propios métodos para redimensionar, sin embargo
la forma mas fácil es con solo CSS (mirar pictures.css.scss)

-Para poder usar la gema rmagick, se tiene que instalar 
imagemagick, rmagick y sus dependencias como libmagick
y otras para que funcione con ruby (hacerlo desde synaptic).
