(I gotten asked this so many times :-) , I figured I would expand my original answer.)

So as an example, in `Debug` mode, I want to include a `Setting.bundle` that consists of `Root.plist` and a submenu `Extra.plist`.

In `Release` mode, I want to include a totally different `Root.plist` and **no** `Extra.plist` in the app's `Setting.bundle`

###My `.csproj` file is going to look like this:

------

      <ItemGroup Condition="'$(Configuration)'!='Debug'">
        <BundleResource Include="Settings.bundle\Root.plist" >
        </BundleResource>
      </ItemGroup>
      <ItemGroup Condition="'$(Configuration)'=='Debug'">
        <BundleResource Include="Settings.debug\Extra.plist" >
        	    <Link>Settings.bundle\Extra.plist</Link>
    	</BundleResource>
        <BundleResource Include="Settings.debug\Root.plist" >
        	    <Link>Settings.bundle\Root.plist</Link>
        </BundleResource>
      </ItemGroup>

------

###Note: 
As shown below, in `Debug` Xamarin is including additional menu items into my Root.plist and in `Release` they are not. Also my `Additional Settings` submenu is no longer available and now are labeled with `XXXX Release`

###Debug mode result:

[![enter image description here][1]][1]

[![enter image description here][2]][2]

##Release mode result:

[![enter image description here][3]][3]


  [1]: http://i.stack.imgur.com/hVYix.png
  [2]: http://i.stack.imgur.com/U4goC.png
  [3]: http://i.stack.imgur.com/8HC9q.png