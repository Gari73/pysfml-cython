.. Copyright 2011 Bastien Léonard. All rights reserved.

.. Redistribution and use in source (reStructuredText) and 'compiled'
   forms (HTML, PDF, PostScript, RTF and so forth) with or without
   modification, are permitted provided that the following conditions are
   met:

.. 1. Redistributions of source code (reStructuredText) must retain
   the above copyright notice, this list of conditions and the
   following disclaimer as the first lines of this file unmodified.

.. 2. Redistributions in compiled form (converted to HTML, PDF,
   PostScript, RTF and other formats) must reproduce the above
   copyright notice, this list of conditions and the following
   disclaimer in the documentation and/or other materials provided
   with the distribution.

.. THIS DOCUMENTATION IS PROVIDED BY BASTIEN LÉONARD ``AS IS'' AND ANY
   EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
   IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
   PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL BASTIEN LÉONARD BE LIABLE
   FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
   CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
   SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
   BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
   WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
   OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION,
   EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.


Graphics
========

.. module:: sf



Misc
----


.. class:: Color(int r, int g, int b[, int a=255])

   Note: this class overrides some comparison and arithmetic operators in the
   same way that the C++ class does..

   The following colors are available as static attibutes, e.g. you can use
   ``sf.Color.WHITE`` to obtain a reference to the white color.

    * BLACK
    * WHITE
    * RED
    * GREEN
    * BLUE
    * YELLOW
    * MAGENTA
    * CYAN

   .. attribute:: r
   .. attribute:: g
   .. attribute:: b
   .. attribute:: a




.. class:: Drawable

   Base class for classes like :class:`Sprite` or :class:`Text`. You
   can create your own drawables by inheriting this class and
   overriding the ``render`` method::

      class Drawable(sf.Drawable):
          def __init__(self):
              self.princess = sf.Sprite(sf.Texture.load_from_file(
                  'examples/princess.png'))
              self.logo = sf.Sprite(sf.Texture.load_from_file(
                  'examples/python-logo.png'))

          def render(self, target, renderer):
              target.draw(self.logo)
              target.draw(self.princess)

   You can then draw the drawable by passing as an argument to
   :meth:`RenderWindow.draw`. For a runnable example, see
   ``examples/customdrawable.py``. There is also a low level rendering
   example in ``examples/lowleveldrawable.py``. For more information,
   read the SFML documentation:
   http://sfml-dev.org/documentation/2.0/classsf_1_1Drawable.php#details.

   .. attribute:: blend_mode
   .. attribute:: color
   .. attribute:: origin
   .. attribute:: position
   .. attribute:: rotation
   .. attribute:: scale

      The object returned by this property will behave, but it might
      be important in some cases to know that its exact type isn't
      tuple, although its class does inherit tuple. In practice it
      should behave just like a tuple, except if you write code that
      checks for exact type using the ``type()`` function. Instead,
      use ``isinstance()``::

        if isinstance(some_object, tuple):
            # We now know that some_object is a tuple

   .. attribute:: x
   .. attribute:: y

   .. method:: tranform_to_local(float x, float y)
   .. method:: transform_to_global(float x, float y)
   .. method:: move(float x, float y)
   .. method:: rotate(float angle)
   .. method:: scale(float x, float y)



.. class:: RenderTarget

   Base class for :class:`RenderWindow` and :class:`RenderTexture`. It
   is abstract; the constructor will raise ``NotImplementedError`` if
   you call it.

   .. attribute:: default_view
   .. attribute:: view

   .. method:: clear
   .. method:: convert_coords
   .. method:: draw
   .. method:: get_viewport
   .. method:: restore_gl_states
   .. method:: save_gl_states



.. class:: IntRect(int left=0, int top=0, int width=0, int height=0)

   You don't have to use this class; everywhere you can pass a
   :class:`IntRect`, you should be able to pass a tuple as
   well. However, it can be more practical to use it, as it provides
   useful methods and is mutable.

   .. attribute:: left
   .. attribute:: top
   .. attribute:: width
   .. attribute:: height

   .. method:: contains(int x, int y)
   .. method:: intersects(IntRect rect[, IntRect intersection])



.. class:: FloatRect(float left=0, float top=0, float width=0, float height=0)

   You don't have to use this class; everywhere you can pass a
   :class:`FloatRect`, you should be able to pass a tuple as
   well. However, it can be more practical to use it, as it provides
   useful methods and is mutable.

   .. attribute:: left
   .. attribute:: top
   .. attribute:: width
   .. attribute:: height

   .. method:: contains(int x, int y)
   .. method:: intersects(FloatRect rect[, FloatRect intersection])



.. class:: Matrix3(float a00, float a01, float a02,\
                   float a10, float a11, float a12,\
                   float a20, float a21, float a22)

   Note: this class overrides the multiplication operator.

   .. attribute:: IDENTITY

      Class attribute containing the identity matrix.

   .. classmethod:: projection(center, size, float rotation)
   .. classmethod:: transformation(origin, translation, float rotation, scale)

   .. method:: __str__()

      Return the content of the matrix in a human-readable format.

   .. method:: get_inverse()
   .. method:: transform()







Image display and effects
-------------------------



.. class:: Shape


   .. attribute:: blend_mode
   .. attribute:: color
   .. attribute:: fill_enabled
   .. attribute:: origin
   .. attribute:: outline_enabled
   .. attribute:: outline_thickness
   .. attribute:: points_count
   .. attribute:: position
   .. attribute:: rotation
   .. attribute:: the_scale
   .. attribute:: x
   .. attribute:: y

   .. classmethod:: line(float p1x, float p1y, float p2x, float p2y,\
                         float thickness, color\
                         [, float outline=0.0[, outline_color]])
   .. classmethod:: rectangle(float left, float top, float width,\
                              float height, color\
                              [, float outline=0.0[, outline_color]])
   .. classmethod:: circle(float x, float y, float radius, color\
                           [, float outline=0.0[, outline_color]])

   .. method:: add_point(float x, float y[, color[, outline_color]])
   .. method:: get_point_color(int index)
   .. method:: get_point_outline_color(int index)
   .. method:: get_point_position(int index)
   .. method:: move(float x, float y)
   .. method:: rotate(float angle)
   .. method:: scale(float x, float y)
   .. method:: set_point_color(int index, color)
   .. method:: set_point_outline_color(int index, color)
   .. method:: set_point_position(int index, float x, float y)
   .. method:: tranform_to_local(float x, float y)
   .. method:: transform_to_global(float x, float y)




.. class:: Image(int width, int height[, color])

   .. attribute:: height
   .. attribute:: width

   .. classmethod:: load_from_file(filename)
   .. classmethod:: load_from_memory(str mem)
   .. classmethod:: load_from_pixels(int width, int height, str pixels)

   .. method:: __getitem__()

      Get a pixel from the image. Equivalent to :meth:`get_pixel()`. Example::

         print image[0,0]  # Create tuple implicitly
         print image[(0,0)]  # Create tuple explicitly

   .. method:: __setitem__()

      Set a pixel of the image. Equivalent to :meth:`set_pixel()`. Example::

         image[0,0] = sf.Color(10, 20, 30)  # Create tuple implicitly
         image[(0,0)] = sf.Color(10, 20, 30)  # Create tuple explicitly

   .. method:: copy(Image source, int dest_x, int dest_y\
                    [, source_rect, apply_alpha])
   .. method:: create_mask_from_color(color, int alpha)
   .. method:: get_pixel(int x, int y)
   .. method:: get_pixels()
   .. method:: save_to_file(filename)
   .. method:: set_pixel(int x, int y, color)
   .. method:: update_pixels(str pixels[, rect])



.. class:: Texture([int width[, int height]])

   This class has been recently introduced in SFML 2. It basically
   replaces the :class:`Image` class, except when you need to access
   or set pixels, which is only possible with Images.

   .. attribute:: MAXIMUM_SIZE
   .. attribute:: height   
   .. attribute:: smooth
   .. attribute:: width

   .. classmethod:: load_from_file(filename[, area])

      *area* can be either a tuple or an :class:`sf.IntRect`.

   .. classmethod:: load_from_image(image[, area])

      *area* can be either a tuple or an :class:`sf.IntRect`.

   .. classmethod:: load_from_memory(bytes data[, area])

      *area* can be either a tuple or an :class:`sf.IntRect`.

   .. method:: bind()
   .. method:: get_tex_coords(rect):

      *rect* can be either a tuple or an :class:`sf.IntRect`.

   .. method:: update(object source, int p1=-1, int p2=-1, int p3=-1, int p4=-1)

      This method can be called in three ways, to be consistent with
      the C++ method overloading::

          update(bytes pixels[, width, height, x, y])
          update(image[, x, y])
          update(window[, x, y])


.. class:: Sprite([texture])

   .. attribute:: blend_mode
   .. attribute:: color
   .. attribute:: height
   .. attribute:: origin
   .. attribute:: position
   .. attribute:: rotation
   .. attribute:: the_scale
   .. attribute:: size
   .. attribute:: texture
   .. attribute:: width
   .. attribute:: x
   .. attribute:: y

   .. method:: __getitem__()

      Equivalent to :meth:`get_pixel()`.

   .. method:: get_sub_rect()

      .. warning::

         This method returns a copy of the rectangle, so code like
         this won't work::

             sprite.get_sub_rect().top = 10

   .. method:: flip_x(flipped)
   .. method:: flip_y(flipped)
   .. method:: move(float x, float y)
   .. method:: resize(float width, float height)
   .. method:: rotate(float angle)
   .. method:: scale(float x, float y)
   .. method:: set_sub_rect(rect)

      *rect* can be either a tuple or an :class:`IntRect`.

   .. method:: set_texture(image[, adjust_to_new_size=False])
   .. method:: transform_to_global(float x, float y)
   .. method:: transform_to_local(float x, float y)



.. class:: Shader

   The constructor will raise ``NotImplementedError`` if called.  Use
   class methods like :meth:`load_from_file()` or :meth:`load_from_memory()`
   instead.

   .. classmethod:: load_from_file(filename)
   .. classmethod:: load_from_memory(str shader)

   .. method:: bind()

   .. method:: set_parameter(str name, float x[, float y, float z, float w])

      After *name*, you can pass as many parameters as four, depending
      on your need.

   .. method:: set_texture(str name)
   .. method:: set_current_texture(str name)
   .. method:: unbind()




.. class:: RenderTexture(int width, int height[, bool depth=False])

   .. attribute:: active
   .. attribute:: default_view
   .. attribute:: height
   .. attribute:: texture
   .. attribute:: smooth
   .. attribute:: view
   .. attribute:: width
    
   .. method:: clear([color])
   .. method:: convert_coords(int x, int y[, view])
   .. method:: create(int width, int height[, bool depth=False])
   .. method:: display()
   .. method:: draw(drawable[, shader])
   .. method:: get_viewport(view)
   .. method:: restore_gl_states()
   .. method:: save_gl_states()




.. class:: Renderer

   .. attribute:: TRIANGLE_LIST
   .. attribute:: TRIANGLE_STRIP
   .. attribute:: TRIANGLE_FAN
   .. attribute:: QUAD_LIST

   .. attribute:: blend_mode
   .. attribute:: color
   .. attribute:: model_view
   .. attribute:: projection
   .. attribute:: shader
   .. attribute:: texture
   .. attribute:: viewport
 
   .. method:: add_vertex(...)

      This method can be called in the same ways as in C++::

         add_vertex(x, y)  # position only
         add_vertex(x, y, color)  # position and color
         add_vertex(x, y, u, v) # position and texture coordinates
         add_vertex(x, y, u, v, color)  # position, texture coordinates and color

   .. method:: apply_color(color)
   .. method:: apply_model_view(matrix)
   .. method:: begin(int value)
   .. method:: clear(color)
   .. method:: end()
   .. method:: initialize()
   .. method:: push_states()
   .. method:: pop_states()
   .. method:: restore_gl_states()
   .. method:: save_gl_states()




Windowing
---------


.. class:: RenderWindow(VideoMode mode, title\
                        [, style[, ContextSettings settings]])

   *style* can be one of:

   ======================= ===========
   Name                    Description
   ======================= ===========
   ``sf.Style.NONE``
   ``sf.Style.TITLEEBAR``
   ``sf.Style.RESIZE``
   ``sf.Style.CLOSE``
   ``sf.Style.FULLSCREEN``
   ======================= ===========

   .. attribute:: active
   .. attribute:: cursor_position
   .. attribute:: default_view
   .. attribute:: framerate_limit
   .. attribute:: frame_time
   .. attribute:: height
   .. attribute:: joystick_threshold
   .. attribute:: key_repeat_enabled
   .. attribute:: opened
   .. attribute:: position
   .. attribute:: settings
   .. attribute:: show_mouse_cursor
   .. attribute:: size
   .. attribute:: system_handle

      Return the system handle as a long (or int on Python 3). Windows
      and Mac users will probably need to cast this as another type
      suitable for their system's API. Please contact me and show me
      your use case so that I can make the API more user-friendly.

   .. attribute:: title
   .. attribute:: vertical_sync_enabled
   .. attribute:: view
   .. attribute:: width

   .. classmethod:: from_window_handle(long window_handle\
                                       [, ContextSettings settings])

      Equivalent to this C++ constructor::

         RenderWindow(WindowHandle, ContextSettings=ContextSettings())

   .. method:: clear([color])
   .. method:: close()
   .. method:: convert_coords(x, y[, view])
   .. method:: create(VideoMode mode, title\
                      [, int style[, ContextSettings settings]])
   .. method:: display()
   .. method:: draw()
   .. method:: get_input()
   .. method:: get_viewport(view)
   .. method:: iter_events()

      Return an iterator which yields the current pending events. Example::
        
         for event in window.iter_events():
             if event.type == sf.Event.CLOSED:
                 # ...

   .. method:: poll_event()
   .. method:: restore_gl_states()
   .. method:: save_gl_states()
   .. method:: set_icon(int width, int height, str pixels)
   .. method:: show(show)
   .. method:: wait_event()




.. class:: ContextSettings(int depth=24, int stencil=8, int antialiasing=0,\
                           int major=2, int minor=0)

   .. attribute:: antialiasing_level
   .. attribute:: depth_bits
   .. attribute:: major_version
   .. attribute:: minor_version
   .. attribute:: stencil_bits



.. class:: VideoMode([width, height, bits_per_pixel=32])

   Note: this class overrides the comparison operators.

   .. attribute:: width
   .. attribute:: height
   .. attribute:: bits_per_pixel

   .. classmethod:: get_desktop_mode()
   .. classmethod:: get_fullscreen_modes()

   .. method:: is_valid()



.. class:: View( )



   .. attribute:: center
   .. attribute:: height
   .. attribute:: rotation
   .. attribute:: size
   .. attribute:: viewport
   .. attribute:: width

   .. classmethod:: from_center_and_size(center, size)

      *center* and *size* can be either tuples or :class:`Vector2f`.

   .. classmethod:: from_rect(rect)

   .. method:: move
   .. method:: reset
   .. method:: rotate
   .. method:: zoom





Text
----


.. class:: Font()

   .. attribute:: DEFAULT_FONT

      The default font (Arial), as a class attribute::

         print sf.Font.DEFAULT_FONT


   .. classmethod:: load_from_file(filename)
   .. classmethod:: load_from_memory(str data)

   .. method:: get_glyph(int code_point, int character_size, bool bold)
   .. method:: get_texture(int character_size)
   .. method:: get_kerning(int first, int second, int character_size)
   .. method:: get_line_spacing(int character_size)



.. class:: Text([string, font, character_size=0])

   *string* can be either a regular string or Unicode. SFML will
   internally store characters as 32-bit integers. A ``str`` object
   will end up being interpreted by SFML as an "ANSI string" (cp1252
   encoding). A ``unicode`` object will be interpreted as 32-bit code
   points, as you would expect.

   .. attribute:: blend_mode
   .. attribute:: color
   .. attribute:: character_size
   .. attribute:: font
   .. attribute:: origin
   .. attribute:: position
   .. attribute:: rect
   .. attribute:: rotation
   .. attribute:: scale
   .. attribute:: string
   .. attribute:: x
   .. attribute:: y

      This attribute can be set as either a ``str`` or ``unicode``
      object. The value retrieved will be either ``str`` or
      ``unicode`` as well, depending on what type has been set
      before. See :class:`Text` for more information.

   .. attribute:: style

      Can be one or more of the following:

      * ``sf.Text.REGULAR``
      * ``sf.Text.BOLD``
      * ``sf.Text.ITALIC``
      * ``sf.Text.UNDERLINED``

      Example::

         text.style = sf.Text.BOLD | sf.Text.ITALIC

   .. method:: tranform_to_local(float x, float y)
   .. method:: transform_to_global(float x, float y)
   .. method:: move(float x, float y)
   .. method:: rotate(float angle)
   .. method:: scale(float x, float y)



.. class:: Glyph

   .. attribute:: advance
   .. attribute:: bounds
   .. attribute:: sub_rect
